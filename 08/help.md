# Scenest场景描述语言介绍

*scenest语言中的场景由以下几个部分组成:*

## 1. 场景（scenario）

一个场景包含7个组成部分:`地图（map）`，`控制车辆（ego vehicle）`，`NPC车辆（npc vehicles）[可选]`，`行人（pedestrians)[可选]`，`障碍物（obstacles）[可选]`，`环境（environment）[可选]`，`交通（traffic）[可选]`,通过`CreateScenario`来创建一个场景：

```text
/*以下通过CreateScenario创造一个scenario的场景，参数分别为
    map：地图
    ego_vehicle:控制车辆
    npc_vehicles:NPC车辆
    pedestrians：行人
    obstacles：障碍物
    env：环境
    traffic：交通
    以上所有的对象将在接下来一一介绍
*/
/*
    允许默认的参数，通过‘{}’指定。例如
    scenario=CreateScenario{
        load(map);
        ego_vehicle;
        {};//默认npc_vehicles
        {}; //默认pedestrians
        {};//默认obstacles
        {};//默认environment
        {};//默认traffic
    };
*/
scenario=CreateScenario{
    load(map);
    ego_vehicle;
    npc_vehicles;
    pedestrians;
    obstacles;
    env;
    traffic;
};
```

## 3. 控制车辆（ego vehicle）

控制车辆由关键字‘AV’指定，控制车辆由两个个部分组成分别是`初始状态（state）`，`目标状态（state）`

```text
/* 以下指定了一个名字为ego_vehicle的控制车辆,初始状态由ego_init_state指定，
    目标状态由ego_target_state指定*/
​
​
ego_vehicle=AV(ego_init_state,ego_target_state);
```

3.1 状态（state）

状态表示一辆车（控制车辆或者NPC车辆）或者行人的状态信息，由三个部分组成：`位置（position）`，`朝向（heading）[可选]`，`速度（speed）[可选]`位置有两种表示方法：坐标与相对于车道（lane）的表示方法，位置还可以设置`坐标参考系（coordinate frame）`,共有三种：`IMU,ENU[默认],WSG84`坐标可以有二维坐标，也可以设置第三维坐标（**注意:为了可以解析，第三个维度必须加上正负号**）例如：

```text
pos=(1,2,+1);//表示坐标为（1,2,+1）的一点
pos=(1,2,-10);//表示坐标为（1,2,-10）的一点
```

朝向:朝向可以设置相对于某点坐标，可以相对于某个具体的车道，也可以相对于控制车辆

```text
ego_init_position=(2,3); //表示坐标为（2,3）的一点
ego_init_position2=".5"->6; //表示相对于车道5距离为6的一点
heading=34 deg related to EGO;//表示相对于控制车辆34度的方向
speed=35; //表示34的速度
ego_init_state=(ego_init_position,heading,speed);//表示一个初始状态，由初始位置，初始朝向，初始速度组成
ego_target_position=(2,4);
ego_target_state=(ego_target_position);//表示目标状态

```

## 4. NPC车辆（NPC vehicles）

你可以设置多个`NPC车辆（NPC vehicle）`共同组成多个NPC车辆列表，单个NPC车辆由关键字`Vehicle`指定，由以下几个部分组成：`初始状态（state），运动路径（vehicle motion），目标状态（state），车辆类型（vehicle type）`

4.1 运动路径（vehicle motion）

运动路径可以指定为`uniform motion`与`waypoint motion`，前者指定一个状态，后者指定一系列的状态来控制NPC车辆的运动轨迹,

```text
    statelist=(state1,state2，state3); //表示一系列的状态，由state1,state2,state3组成
    uniform=U(state); //表示以给定的状态匀速运动
    waypoint=WP(statelist);//表示一系列的状态运动
    npc1=Vehicle(state1,uniform,state2,vehicle_type);//表示一辆NPC车辆
    npc_vehicles={npc1,npc2};//表示多辆NPC车辆
```

## 5. 行人（pedestrians）

你可以设置多个`行人（pedestrian）`，每一个行人由`Pedestrian`关键字指定，并由`初始状态（state），行人路径（pedestrian motion），目标状态（state），行人类型（pedestrian type）`组成

5.1 行人路径

行人路径与`vehicle motion`一样设置

5.2 行人类型（pedestrian type）

行人类型由`高度（height）`与`颜色（color）`组成

```text
height=1.8;
color=white;
pedestrian_type=(height,color);//表示一个身高1.8,颜色为白色的行人类型
pedestrian1=Pedestrian(state1,uniform,state2,pedestrian_type);//表示一个行人
pedestrians={pedestrian1,pedestrian2};//表示多个行人
```

## 6. 障碍物(obstacles)

你可以设置多个`障碍物（obstacle）`，每个障碍物由关键字`Obstacle`指定，并由`位置（position），形状（shape）`组成

6.1 形状（shape）

形状只有预设的形状：`球（sphere），立方体（box），圆锥（cone），圆柱（cylinder）`

```text
position=(1,2);
box_shape=(box,1,1,1);//表示一个立方体障碍物，长宽高为1,1,1
obstacle1=Obstacle(position,box_shape);//构造一个障碍物
obstacles={obstacle1,obstacle2};//表示多个障碍物
```

## 7. 环境（environment）

环境由关键字`Environment`指定，并由`时间（time），天气（weathers）`组成

7.1 天气（weathers）

你可以制定多个`天气（weather）`条件，格式如下`kind:value`或者`kind:level`其中`kind`可以是`sunny,rain,snow,fog,wetness`,`value`介于0-1之间用来描述程度，或者使用`light，middle，heavy`来指定等级（level）

```text
time=12:00;
weather1=rain:0.1;
weather2=fogness:middle;
weathers={weather1,weather2};//指定多个天气条件
env=Environment(time,weathers);//指定环境
```

## 8. 交通（traffic）

交通由车道`交汇路口交通情况（intersection traffic）`与`车道限速（speed limitation）`组成。交汇路口的交通情况可以指定交汇路口的`交通灯（traffic light），停止信号（stop sign），人行横道（crosswalk）`格式如下：`Intersection(intersection id,traffic light,stop sign,crosswalk)`车道（lane）的限速情况：`SpeedLimit(lane id,(speed-min,speed-max)`

```text
intersection1=Intersection(3,0,0,0);
intersection2=Intersection(6,1,1,0);
speedlimit1=(1,(80,120));//表示车道1的限速情况
traffic={intersection1,intersection2,speedlimt1};
```

## 其它

注释：允许行内与块内注释，以`//`和`/**/`方式声明

## 一个完整的实例

 下面是一个完整的实例：

```text
    map = "San Francisco";//地图名字
    ego_init_position = (4.5, 214);
    ego_target_position = (4.5, -200);
    ego_init_state = (ego_init_position);
    ego_target_state = (ego_target_position);
    car_model = "Lincoln MKZ 2017";//车辆具体类型
    car_color = (255, 0, 0);
    vehicle_type = (car_model, car_color);//使用car_model,car_color来标识车辆类型（vehicle type）
    ego_vehicle = AV(ego_init_state, ego_target_state, vehicle_type);//创建一个ego vehicle
    npc_init_state = (".1"->0.0, ,1.5) ;//创造一个状态，该状态有一个位置为".1"->0.0，默认朝向，，速度为1.5
    motion = U(npc_init_state);//使用npc_init_state来创造一个uniform motion
    npc1 = Vehicle(npc_init_state, motion);//使用motion和npc_init_state来创造一个npc1
    npc_init_state2 = ("2"->0.0, ,1.0);//创造npc_init_state2状态
    npc_state = (("2"->0.0, , 1.0), ("2"->50.0, ,1.0));//创造状态列表（state list），该列表有两个匿名状态组成
    npc2 =Vehicle(npc_init_state2, Waypoint(npc_state), ("4"->100, ,0.0), vehicle_type);//创造第二辆npc2
    heading = 45 deg related to EGO;
    npc_init_state3 = ((9.5, 114), heading, 0.0);
    npc3 = Vehicle(npc_init_state3);//创造第三辆npc3
​
    npc = {npc1, npc2, npc3};//创造npc车辆，共有三辆车
​
    pedestrian_type = (1.65, black);
    pedestrian = Pedestrian(((19,13), ,0.5), , ((0,13), ,0), pedestrian_type);//创造一个行人
    pedestrians={pedestrian};//创造行人列表，只有一个行人
    time = 10:00;
    weather = {rain: 0.1};
    env = Environment(time, weather);//添加天气信息
​
    speed_range = (0,20);
    speed_limit = SpeedLimit(5, speed_range);
    i1 = Intersection(1, 1, 0, 1);
    traffic = {i1,speed_limit};//创造traffic约束
​
    scenario = CreateScenario{load(map);
                        ego_vehicle;
                        npc;
                        pedestrians;
                        {};//默认的障碍物（obstacles）
                        env;
                        traffic;
    };//使用map,ego_vehicle,npc,pedestrians,env,traffic来创建一个场景，名字为scenario
```



