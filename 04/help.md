# 快速上手

## 流程概览

![image-20220304170444003](..\picture\1.png)



## 完整仿真测试流程

仿真测试分为3步主要流程：创建测试作业、执行测试作业、查看测试结果。

### 创建测试作业

点击左侧导航栏【作业管理】按钮，进入作业管理列表界面。

![image-20220304184353260](..\picture\2.png)

点击右侧【新建】按钮，进入作业详情界面。

![image-20220304184419980](..\picture\3.png)

填写作业名称后，点击“任务执行单元”中的【增加】按钮进入”创建任务执行单元“页面，批量创建任务。

![image-20220304184444056](..\picture\4.png)

进入”任务执行单元“页面后，需依次选择场景、受测车辆：

点击场景右侧【修改】按钮下方将显示场景库及已选场景，勾选场景后点击【增加】按钮后完成场景选择；

点击”受测车辆“下拉按钮，选择选择任务测试车辆；

完成后点击【确定】按钮完成任务批量创建。

![image-20220304184521506](..\picture\5.png)

点击【保存】按钮，完成测试作业创建工作。

### 执行测试作业

点击导航栏【仿真测试】按钮，进入仿真测试作业列表。

![image-20220304190240970](..\picture\6.png)

点击勾选按钮，选择目标作业后，点击【执行】按钮，完成测试作业执行工作。

### 查看测试结果

点击导航栏【仿真测试】按钮，进入仿真测试作业列表。

![image-20220304190240970](..\picture\17.png)

选择已完成作业，点击【作业名称】或右侧详情【编辑】按钮，进入作业详情页面

![image-20220304190254626](..\picture\18.png)

点击任务”得分“列内的【分数】，可通过弹窗查看任务得分详情项。

![image-20220304190308656](..\picture\19.png)

点击任务”操作“列的【日志】，可通过弹窗查看任务执行日志。

![image-20220304190329778](..\picture\20.png)

点击任务”操作“的【回放】，可通过弹窗查看任务执行视频回放。

![image-20220304194524492](..\picture\21.png)



## 创建测试车辆

创建测试车辆主要流程为：创建车辆→填写基本信息→选择车辆控制系统→选择车身模型→选择动力学模型→搭载传感器

### 如何创建测试车辆

· 点击导航栏中【车辆管理】.车辆列表页面，需点击【新建】按钮，创建自己的自动驾驶车辆。

![image-20220304180021351](..\picture\7.png)

· 依次输入“车辆名称”、选择“车身模型”、“车灯状态”、”车身颜色“，后选择“控制系统”、”动力学模型“、”传感器模型“后点击【保存】按钮，完成车辆创建。![image-20220304180119790](..\picture\8.png)

点击【完成】完成车辆创建。

### 如何创建动力学模型

点击左侧导航栏【资源库】按钮，进入资源库页面。

![image-20220304180935730](..\picture\zy.png)

点击”主车资源“下的【动力学模型】按钮，进入动力学模型列表页面。

![image-20220304180935730](..\picture\dl.png)

点击【创建】按钮，进入车辆动力学模型详情界面。

![image-20220304181032168](..\picture\9.png)

依次输入模型名称”，修改参数信息后点击【保存】按钮，完成车辆动力学模型创建。

### 如何创建传感器模型

点击左侧导航栏【资源库】按钮，进入资源库页面。

![image-20220304180935730](..\picture\zy.png)

点击”主车资源“下的【传感器模型】按钮，进入传感器模型列表页面。

![image-20220304181230260](..\picture\cg.png)

点击【创建】按钮，进入轮胎动力学模型详情界面。

![image-20220304181326975](..\picture\10.png)

输入“模型名称”，修改参数信息后点击【保存】按钮，完成轮胎动力学模型创建。



## 如何创建测试场景

点击左侧导航栏【场景管理】按钮，进入场景列表页面。

![image-20220304184041341](..\picture\11.png)

点击界面右侧的【创建】按钮，进入场景详情。

![image-20220304184123768](..\picture\12.png)

依次填写“场景名称”、场景配置中”动态场景描述“、”场景天气“、”运行地图“后，点击【保存】按钮完成场景创建。

### 如何创建场景天气

点击左侧导航栏【资源库】按钮，进入资源库页面。

![image-20220304180935730](..\picture\zy.png)

点击”场景资源“下的【场景天气】按钮，进入场景天气列表页面。

![image-20220304184247035](..\picture\13.png)

点击【创建】按钮，进入天气详情界面。

![image-20220304184305665](..\picture\14.png)

依次填写天气名称、参数信息中各参数后，点击【保存】完成天气创建。

### 如何创建场景脚本

点击左侧导航栏【资源库】按钮，进入资源库页面。

![image-20220304180935730](..\picture\zy.png)

点击”场景资源“下的【动态场景描述】按钮，进入动态场景描述列表页面。

![image-20220304184320270](..\picture\15.png)

点击【新建】按钮进入场景脚本详情。

![image-20220304184333870](..\picture\16.png)

依次输入动态场景描述名称、脚本类型，脚本编码内容后点击【保存】完成脚本创建。

备注：脚本描述语法规则，前往”动态场景描述“查看。  
