# Scenest断言描述介绍

*scenest语言中的断言由以下几个部分组成*

## 1 规划路径（Trace） 

 每一个场景都对应一条规划路径，例如，通过语法

```text
 Trace trace=EXE(scenario);
```

 表示将场景*scenario*关联到名字为*trace*的路径上。 规划路径代表着车辆一系列的状态，可以获取某一时刻的状态， 规划路径某一时刻的状态包括控制车辆的状态，NPC车辆的状态等等 我们可以获取这些信息，取如下形式

```text
 <ego-state> =<trace-state>[ego]
 <trace-state> ::=<trace-id>[time]
```

 *trace-state*表示规划路径某一状态 例如：

```text
    ego-state=trace[1][ego];
```

表示将规划路径*trace*时刻1的控制车辆信息赋值给变量*ego-state*把一辆*NPC*车辆，一个障碍物，或者一个行人对象都称为一个agent对象，因此也可以获取它们的信息，例如：

```text
agent-state=trace[1][perception][agent-name];
```

上面的代码中，解析器将会寻找名字为*agent-name*的对象，可以是一个NPC车辆，一个障碍物，或者一个行人，并把规划路径*trace*时刻1的有关的**感知**信息信息赋值给变量*agent-state*.也可以获取**实际**状态，例如：

```text
agent-ground-truth=trace[1][truth][agent-name];
```

上面的代码中，解析器将会寻找名字为*agent-name*的对象，可以是一个NPC车辆，一个障碍物，或者一个行人，并把规划路径*trace*时刻1的有关的**实际**信息信息赋值给变量*agent-ground-truth*.

有关perception与truth的概念，请参考*autoware自动驾驶*

## 2 断言（Assertion）

断言表示期望一条规划路径上满足的某些性质。

断言的语义基于[MTL operators](https://github.com/mvcisback/py-metric-temporal-logic)

### 2.1 检测断言（Detection Assertion）

检测断言分为关于agent的检测断言（Agent Detection）与交通感知断言（Traffic Detection）

2.1.1 关于agent的检测断言（Agent Detection）

分为agent感知断言与agent误差断言，通过以下方法规定一个感知断言

> 

其中，*ego-state*表示某时刻控制车辆的状态，*agent-ground-truth*表示某个*agent*实际状态，它们必须在感知范围内，*sensing-range*是一个实数

*agent-ground-truth*是*agent*实际状态，语法在上面以给出相比之前的*agent-state*，这里只需要把*perception*换成*truth*

agent误差断言表示，表示感知与实际的误差范围在允许范围之内，取如下形式：

```text
diff(<agent-state,agent-ground-truth)<= <threshold>
```

其中，*agent-state*与*agent-ground-truth*上面已给出定义，这个断言表示的是感知到的agent状态和实际的agent状态误差小于等于*threshold*表示的值

2.1.2 交通感知断言(Traffic Detection)

表示感知与实际的交通情况相同，取如下形式：

```text
<trace-state>[perception][traffic]==<trace-state>[truth][traffic]
```

其中，<trace-state>表示规划路径的某一时刻，上面已经给出

### 2.2 安全断言（Safety Assertion）

安全断言由关于agent的检测断言与安全距离断言组成，表示安全的距离断言取如下形式：

```text
dis(<ego-state>,<agent-state>)>= <safety-radius>
```

表示感知到的*ego*车辆与*agent*对象，距离必须满足给定的要求，*safety-radius*给出表示安全距离的实数

### 2.3 交通断言（Intersection Assertion）

如下形式：

```text
(<traffic-detection>&<red-light>)->(~<ego-speed>U(<traffic-detection>&<green-light>))
<red-light> ::=<trace-state>[traffic]==red
<green-light> ::=<trace-state>[traffic]==green
<ego-speed> ::=norm(<ego-velocity)
<ego-velocity> ::=<coordinate>
```

其中，*traffic-detection*上面已给出，而*red-light*与*green-light*表示检测到红灯与绿灯状况。*ego-speed*表示*ego*车辆的速度，[*coordinate*](./scenest-scenario.md)在场景文法中已给出。

此断言表示，检测的交通状况断言，在遇到红灯的情况下，*ego-speed*表示的速度一定为0,直到检测的交通状况为绿灯

### 2.4 速度约束断言（Speed Constraint Assertion）

取如下形式：

```text
(<traffic-detection>&<speed-limitation-checking>&<speed-violation>)->F[0,<time-duration>]~<speed-violation> 
<speed-limitation-checking>::=<trace-state>[traffic]==<speed-range>
<speed-violation>::=<speed><trace-state>[traffic][0]
```

其中，[*speed-range*与*speed*](./scenest-scenario.md)在之前的场景文法中已给出

该断言表示，检测到的交通断言，如果存在速度检查（*speed-limitation-checking*）以及速度违反检测(*speed-violation*)的限制，则在时刻0到由实数*time-duration*给定的值时刻之内不能违反第二个速度违反断言

## 3. 断言附加到规划路径上

   四种断言（检测断言，安全断言，交通路口断言，速度约束断言）在描述之后，必须附加到给出的规划路径上，表示在这个规划路径上断言生效，通过下面的方式：

```none
   <trace-id>|=G<detection-assertion> //<detection-assertion>表示检测断言，假设在此之前已给出
   <trace-id>|=G<safety-assertion> //<safety-assertion>表示安全断言，假设在此之前已给出
   <trace-id>|=G<intersection-assertion> //<intersection-assertion>表示交通路口断言，假设在此之前已给出
   <trace-id>|=G<speed-constraint-assertion> //<speed-constraint-assertion>表示速度约束断言，假设在此之前已给出
```

下面是一个例子，包含了以上所有的断言内容：

```text
Trace trace=EXE(scenario);// 由场景scenario给出一个执行路径trace
ego_vehicle_state= trace[1][ego];// 从场景时刻1中提取控制车辆信息
npc_vehicle1= trace[1][perception][npc1];//从场景时刻1提取名字为npc1的感知信息
npc_vehicle1_ground= trace[1][truth][npc1];//从场景时刻1提取名字为npc1的实际信息
npc_vehicle2= trace[1][perception][npc2];//从场景时刻1提取名字为npc2的感知信息
npc_vehicle2_ground = trace[1][truth][npc2];//从场景时刻1提取名字为npc2的实际信息
npc_vehicle3= trace[1][perception][npc3];//从场景时刻1提取名字为npc3的感知信息
npc_vehicle3_ground =  trace[1][truth][npc3];//从场景时刻1提取名字为npc3的实际信息
pedestrian_truth = trace[1][perception][pedestrian];//从场景时刻1提取名字为pedestrian的感知信息
pedestrian_ground = trace[1][truth][pedestrian];//从场景时刻1提取名字为pedestrian的实际信息
​
dis1 = dis(ego_vehicle_state, npc_vehicle1_ground);
error = diff(npc_vehicle1, npc_vehicle1_ground);
perception_detection = dis1<= 0.1 & error <= 0.1;//定义一个包含agent感知断言与agent误差断言的检测断言
trace |=G perception_detection ;// 断言附加到路径上
trace |=G dis1<= 0.1 & error <= 0.1 & dis(ego_vehicle_state, npc_vehicle1)>= 0.1 ; //定义一个包含agent感知断言，agent误差断言和安全距离断言的安全断言，并附加到路径上
intersection_assertion=(trace[1][perception][traffic]==trace[1][truth][traffic]
    &trace[1][traffic]==red)->(~norm((100,100))U(trace[1][perception][traffic]==trace[1][truth][traffic]
    &trace[1][traffic]==green));//定义一个交通断言
trace |=G intersection_assertion;// 断言附加到路径上
// speed constraint assertion
speed_constraint_assertion=(trace[1][perception][traffic]==trace[1][truth][traffic]
    &trace[1][traffic]==(100,200)&120<trace[1][traffic][0])
    ->F[0,2]~120<trace[1][traffic][0];//定义一个速度约束断言
trace |=G speed_constraint_assertion;// 断言附加到路径上
```

