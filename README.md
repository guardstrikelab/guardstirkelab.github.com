# 版本说明
【版本发布的说明，包含每个版本新增功能、已有功能优化、Bug修复、及其它版本修改内容说明。倒叙记录，版本号越高在此文档中位置越靠前】

## v0.3.1-beta

### 新增功能

·增加测试日志功能，打印任务执行整个流程的状态信息。

### 功能优化

· 界面UI配色重新设计。

· 解决若干稳定性问题。

· 解决若干部署问题。

# 概述

## 关于GuardStrike

深信科创由软件领域国际知名学者杨子江教授创建，经清华大学交叉信息学院孵化成立于2019年。公司致力于自动驾驶安全解决方案，从算法研发到工程实现上为安全出行保驾护航。成立伊始，深信科创已经成为国家高新技术企业，并与工信部中国电子技术标准化研究院、公安部一所、国家金融科技评测中心、长安汽车、大连人工智能研究院等机构成立联合实验室。携手工信部四院，深信科创牵头发布了有华为、商汤、百度、中科院软件所、中汽研等单位参与的自动驾驶场景描述语言白皮书。在国家智能网联汽车研究院和清华长三角研究院战略投资，及北京将门、青岛润扬，杭州度岩财务投资协助下，深信科创力争让安全事故仅发生在虚拟世界，成为独树一帜的自动驾驶EDA企业。

## 关于Oasis

· 深信科创自动驾驶仿真测试云平台OASIS，采用云原生架构，可以进行公有云及私有云的部署。由于软件系统复制几乎没有成本，在OASIS上进行大规模测试仅受算力成本的约束。OASIS通过场景描述及算法学习能力，可以产生大量corner cases以达到提升测试效率的目的。

· 具备构建高保真测试场景的能力,并且可以配合车厂及研究人员进行深度定制化开发，将仿真测试能力整合入自动驾驶感知、决策规划和控制全栈算法的全流程，降低自动驾驶算法开发的投入成本，加速自动驾驶算法的研发工作。

# 推荐配置

| 服务名称                                 | 服务版本   | 操作系统    | CPU | 内存 | 显存   |
| ---------------------------------------- | ---------- | ----------- | --- | ---- | ------ |
| Carla                                    | 0.9.10     | ubuntu18.04 | 8核 | 32G  | 12-16G |
| sdg engine                               | 0.3.1-beta | ubuntu18.04 | 8核 | 16G  |        |
| sdg-carla-ros-bridge，sdg-autoware-agent | 0.3.1-beta | ubuntu18.04 | 8核 | 16G  |        |
| Autoware                                 | 1.4        | ubuntu18.04 | 8核 | 32G  | 12-16G |
| sdg-server                               | 0.3.1-beta | ubuntu18.04 | 4核 | 8G   |        |
| sdg-web                                  | 0.3.1-beta | ubuntu18.04 | 4核 | 8G   |        |
| sdg-replay                               | 0.3.1-beta | ubuntu18.04 | 4核 | 8G   |        |
| sdg-task-listener                        | 0.3.1-beta | ubuntu18.04 | 8核 | 32G  |        |

# 使用说明

流程概览

![](https://tcs-devops.aliyuncs.com/storage/112f47c68c0ee4a12fc94c8a6d5a4644d99b?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmY0N2M2OGMwZWU0YTEyZmM5NGM4YTZkNWE0NjQ0ZDk5YiJ9.w-FpvyeW3pgp31OT9UEBTHzRXMPuH1Q0lRpGE4RA7_w&download=image-20220304170444003.png "")

## 完整车辆创建流程

1 创建受测车辆。

2 创建动力学模型。

3 为各轮胎创建轮胎动力学模型。

4 创建必要的传感器模型。

5 进入车辆详情页面完成车辆装配：车辆动力学模型、轮胎动力学模型、传感器模型。

### 如何创建受测车辆

· 进入系统默认进入测试车辆.车辆列表页面，需点击【新建】按钮，创建自己的自动驾驶车辆。

![](https://tcs-devops.aliyuncs.com/storage/112f5375003efe5bf401a57737df6e8ab385?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmY1Mzc1MDAzZWZlNWJmNDAxYTU3NzM3ZGY2ZThhYjM4NSJ9.in2qXQh0PckP2CfOJ0x6MFfWZlMBBVCbXn7X4xm073A&download=image-20220304180021351.png "")

· 依次输入“车辆名称”、选择“车辆模型”、“车灯状态”、”车身颜色“，设置车辆基本信息

![](https://tcs-devops.aliyuncs.com/storage/112f466a261611448b70660e0b0dcee8a176?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmY0NjZhMjYxNjExNDQ4YjcwNjYwZTBiMGRjZWU4YTE3NiJ9.tP7pXsrXFhQ5Fd0_VNG7mgCEPO9ClNKrzDHMDdqRgXM&download=image-20220304180119790.png "")

点击【完成】完成车辆创建。

### 如何创建动力学模型

点击左侧导航栏【车辆动力学】按钮，进入动力学模型列表。

![](https://tcs-devops.aliyuncs.com/storage/112fc9c425f1d070894f43657bb4ccf31f97?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmZjOWM0MjVmMWQwNzA4OTRmNDM2NTdiYjRjY2YzMWY5NyJ9.pIjLuSZtlBxn1z29qN_7vRXPXs6VfNkpDu8ZTi9daxQ&download=image-20220304180935730.png "")

点击【新建】按钮，进入车辆动力学模型详情界面。



依次输入/下拉选择“车辆动力学模型名称”、“所属车辆”，修改参数信息后点击【保存】按钮，完成车辆动力学模型创建。

### 如何创建轮胎动力学模型

点击左侧导航栏【轮胎动力学】按钮，进入动力学模型列表。

![](https://tcs-devops.aliyuncs.com/storage/112f81a3f8d5aa6372531636cb1e7a89ed13?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmY4MWEzZjhkNWFhNjM3MjUzMTYzNmNiMWU3YTg5ZWQxMyJ9.vuupgz-J_-IE9ajWc8ochvIKxTYEBOL04BgG2HBoacY&download=image-20220304180935730.png "")

点击【新建】按钮，进入轮胎动力学模型详情界面。

![](https://tcs-devops.aliyuncs.com/storage/112f1c8cbc4006e2f78f84146a43b2816a2a?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmYxYzhjYmM0MDA2ZTJmNzhmODQxNDZhNDNiMjgxNmEyYSJ9.HMMxp4ITwl0Sp-4ZvAhbfyr-ZFfb2ne3jRthrcU5iYI&download=image-20220304181032168.png "")

依次输入/下拉选择“轮胎动力学模型名称”、“所属车辆”，修改参数信息后点击【保存】按钮，完成轮胎动力学模型创建。

### 如何创建传感器模型

点击左侧导航栏【传感器模型】按钮，进入传感器模型列表。

![](https://tcs-devops.aliyuncs.com/storage/112f6d8ba909a1368a7b2d98b84262f66570?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmY2ZDhiYTkwOWExMzY4YTdiMmQ5OGI4NDI2MmY2NjU3MCJ9.t0siIJRGY1xmH5uQ69EjDVcQjpReWpzF5DJM9mn3qXE&download=image-20220304181524807.png "")

点击【新建】按钮，进入传感器模型详情界面。

![](https://tcs-devops.aliyuncs.com/storage/112f8f81e529735ed2d1d0171c8529da5dce?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmY4ZjgxZTUyOTczNWVkMmQxZDAxNzFjODUyOWRhNWRjZSJ9.aG0I6HgneiaQSG7HoXz7uDKKy5sX31erFcBb-D9LHRo&download=image-20220304181802645.png "")

依次输入/下拉选择“传感器模型名称”、“类型”、“所属车辆”，修改参数信息后点击【保存】按钮，完成传感器模型创建。

### 如何完成车辆模型装配

车辆需完成动力学模型、轮胎动力学模型、传感器模型的装配后方可用于仿真测试。

点击左侧导航栏【测试车辆】.【车辆列表】按钮，进入车辆列表页面。

![](https://tcs-devops.aliyuncs.com/storage/112ff95226aefbfb10900c11227d17ae83eb?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmZmOTUyMjZhZWZiZmIxMDkwMGMxMTIyN2QxN2FlODNlYiJ9.ojhzaqa6D-7zn_rbD52kN9-LfzEP-roIq_nWYda6aYQ&download=image-20220304182753898.png "")

点击所选车辆右侧的【详情】按钮，进入车辆详情。

![](https://tcs-devops.aliyuncs.com/storage/112f6ad2c26cbfa706b5018aed1c1e4fe03b?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmY2YWQyYzI2Y2JmYTcwNmI1MDE4YWVkMWMxZTRmZTAzYiJ9.pwTaCxly4KQKY3cTD2_jV4uglhaUPkedx7R2xgNuNdE&download=image-20220304183015336.png "")

依次下拉选择已创建的“车辆动力学”、每个位置的“轮胎动力学”，可点击【增加】为车辆新创建一个传感器并依次选择类型、名称完成选装传感器。

完成配置工作后点击【保存】完成车辆装配全部工作。

## 如何创建测试场景

点击左侧导航栏【场景管理】.【场景列表】按钮，进入场景列表页面。

![](https://tcs-devops.aliyuncs.com/storage/112ff2f05dee711306b232e8aeaaa6b02370?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmZmMmYwNWRlZTcxMTMwNmIyMzJlOGFlYWFhNmIwMjM3MCJ9.k4KsQI4GvnvMumIFn3sG_TGYPIISkMq0fBo8OD4jQQ0&download=image-20220304184041341.png "")

点击界面右侧的【新建】按钮，进入场景详情。

![](https://tcs-devops.aliyuncs.com/storage/112fd3337c2984e2ea33016892b061a56c84?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmZkMzMzN2MyOTg0ZTJlYTMzMDE2ODkyYjA2MWE1NmM4NCJ9.Gr0e2-kJQwflc5vv3b8D8gsmlG7bipzokURtt85hvok&download=image-20220304184123768.png "")

依次填写/下拉选择“场景名称”、参数信息中”地图“、”天气“、”脚本“后，点击【保存】按钮完成场景创建。

### 如何创建场景天气

点击左侧导航栏【场景天气】按钮，进入场景天气列表页面。

![](https://tcs-devops.aliyuncs.com/storage/112f7d610d66b8671d22b1457af0882039c0?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmY3ZDYxMGQ2NmI4NjcxZDIyYjE0NTdhZjA4ODIwMzljMCJ9.xlB7ZQFGtkNH5krEAUJqiLw2joPseSivCLwnnIsy92k&download=image-20220304184247035.png "")

点击【新建】按钮，进入天气详情界面。

![](https://tcs-devops.aliyuncs.com/storage/112f8fb5b8e846f3646f6ef09292420597f9?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmY4ZmI1YjhlODQ2ZjM2NDZmNmVmMDkyOTI0MjA1OTdmOSJ9.IfdrFurdUC-UHW4vecOl6QAltjE0SkvBT5t5sJg9AmA&download=image-20220304184305665.png "")

依次填写天气名称、参数信息中各参数后，点击【保存】完成天气创建。

### 如何创建场景脚本

点击左侧导航栏【场景脚本】按钮，进入场景脚本列表页面。

![](https://tcs-devops.aliyuncs.com/storage/112f68282f55475b8560cbc9603bda2afb09?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmY2ODI4MmY1NTQ3NWI4NTYwY2JjOTYwM2JkYTJhZmIwOSJ9.JmB4C1wiQl_VwL--Va_wuGzMx6c1pn144Ze9pXet3Ko&download=image-20220304184320270.png "")

点击【新建】按钮进入场景脚本详情。

![](https://tcs-devops.aliyuncs.com/storage/112fa9e4232581fbcd859d632949aabd8498?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmZhOWU0MjMyNTgxZmJjZDg1OWQ2MzI5NDlhYWJkODQ5OCJ9.sdAwrie-mPXt1o8wkS-YbrAXFQ79rQItJPB-Gs6xuis&download=image-20220304184333870.png "")

依次输入脚本名称、脚本内容后点击【保存】完成脚本创建。

备注：脚本描述语法规则，前往”动态场景描述“查看。  

## 如何进行仿真测试

仿真测试分为3步主要流程：创建测试作业、执行测试作业、查看测试结果。

### 创建测试作业

点击左侧导航栏【仿真测试】按钮，进入仿真测试作业列表界面。

![](https://tcs-devops.aliyuncs.com/storage/112f5d4e20c676f6012d58a0dd8cff08d413?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmY1ZDRlMjBjNjc2ZjYwMTJkNThhMGRkOGNmZjA4ZDQxMyJ9.iTfNjRvPxC2iE7BLqjL25gDGqVQZyo0O0dGL2FUUsTQ&download=image-20220304184353260.png "")

点击右侧【新建】按钮，进入作业详情界面。

![](https://tcs-devops.aliyuncs.com/storage/112fe23c8444113acc588b8ebd2b9a9cd040?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmZlMjNjODQ0NDExM2FjYzU4OGI4ZWJkMmI5YTljZDA0MCJ9.dz0yDh1-mvNCr85bAk4biHaSUzcbZHlpG_xBRT2Cmno&download=image-20220304184419980.png "")

依次填写作业名称后，点击【增加】按钮进入”批量创建测试任务“页面，批量创建任务。

![](https://tcs-devops.aliyuncs.com/storage/112f94fcc761b35a729e772d06a900e99119?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmY5NGZjYzc2MWIzNWE3MjllNzcyZDA2YTkwMGU5OTExOSJ9.RHRapMKny1MTnkZ6U0m7ExN1C-aJkgbB7IVYUTrGokc&download=image-20220304184444056.png "")

进入”批量创建测试任务“后，需依次选择场景、受测车辆：

点击场景右侧【修改按钮】下方显示场景库及已选场景，勾选场景后点击【增加】按钮后完成场景选择；

点击”受测车辆“下拉按钮，选择选择任务车辆；

完成后点击【确定】按钮完成任务批量创建。

![](https://tcs-devops.aliyuncs.com/storage/112fe20c9e0721d87d37d900382982fa6fde?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmZlMjBjOWUwNzIxZDg3ZDM3ZDkwMDM4Mjk4MmZhNmZkZSJ9.yXQ6fniqFMN52giZVWF29cInP6ll7-RO-UJQFhQ6KuY&download=image-20220304184521506.png "")

点击【保存】按钮，完成测试作业创建工作。

### 执行测试作业

点击导航栏【仿真测试】按钮，进入仿真测试作业列表。

![](https://tcs-devops.aliyuncs.com/storage/112f831d2ddaaad31680d5d1f7cbdd16df77?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmY4MzFkMmRkYWFhZDMxNjgwZDVkMWY3Y2JkZDE2ZGY3NyJ9.t51REXuYpQQYLP2rn7HsbHgmo92jUEH51ea2ind2g08&download=image-20220304190240970.png "")

点击勾选按钮，选择目标作业后，点击【执行】按钮，完成测试作业执行工作。

### 查看测试结果

点击导航栏【仿真测试】按钮，进入仿真测试作业列表。

![](https://tcs-devops.aliyuncs.com/storage/112f831d2ddaaad31680d5d1f7cbdd16df77?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmY4MzFkMmRkYWFhZDMxNjgwZDVkMWY3Y2JkZDE2ZGY3NyJ9.t51REXuYpQQYLP2rn7HsbHgmo92jUEH51ea2ind2g08&download=image-20220304190240970.png "")

点击已完成作业的【作业名称】或右侧【查看】按钮，进入作业详情页面

![](https://tcs-devops.aliyuncs.com/storage/112fb29d7d0c5a018628cbb1448d811cd7bd?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmZiMjlkN2QwYzVhMDE4NjI4Y2JiMTQ0OGQ4MTFjZDdiZCJ9.Ay7Izid5b8CYdnKOZ9LYMx_OUI3AGCzqKO9IWL3Lfog&download=image-20220304190254626.png "")

点击任务”得分“列内的【分数】，可通过弹窗查看任务得分详情项。

![](https://tcs-devops.aliyuncs.com/storage/112f6abdf7aa6eba33232f4d01d8b08eab79?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmY2YWJkZjdhYTZlYmEzMzIzMmY0ZDAxZDhiMDhlYWI3OSJ9.oivHxbfOcCoCVz0OKdmkoEA9UWWpR9QnL0Ixi-M-m64&download=image-20220304190308656.png "")

点击任务”操作“列的【日志】，可通过弹窗查看任务执行日志。

![](https://tcs-devops.aliyuncs.com/storage/112f2965ad76501c9e7278cd76e65a8e97fd?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmYyOTY1YWQ3NjUwMWM5ZTcyNzhjZDc2ZTY1YThlOTdmZCJ9.snsD40jeDsJjhGrJc9Gwu4_4IzLu1ceqdheEtGUmxxY&download=image-20220304190329778.png "")

点击任务”操作“的【回放】，可通过弹窗查看任务执行视频回放。

![](https://tcs-devops.aliyuncs.com/storage/112f79a46d3ef1bc8a4f026ae493e58ad185?Signature=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJBcHBJRCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9hcHBJZCI6IjVlNzQ4MmQ2MjE1MjJiZDVjN2Y5YjMzNSIsIl9vcmdhbml6YXRpb25JZCI6IiIsImV4cCI6MTY0Nzg1NDM5NSwiaWF0IjoxNjQ3MjQ5NTk1LCJyZXNvdXJjZSI6Ii9zdG9yYWdlLzExMmY3OWE0NmQzZWYxYmM4YTRmMDI2YWU0OTNlNThhZDE4NSJ9.B5lfPAJA5MPhsQSMQK0kYG2pXaxyadyZOYed2wJjQmI&download=image-20220304194524492.png "")

# 其它

## 如何接入车辆控制系统

系统初始化已预置Autoware操作系统，平台暂不支持自动导入自动驾驶系统。

如需接入其它操作系统，需后台手动对接，具体请联系我司商务人员。

## 如何导入车辆模型

系统初始化已预置18辆不同的小型汽车供使用，平台暂不支持自动导入车辆模型。

如需接入其它车辆模型，需后台手动对接，具体请联系我司商务人员。

## 如何导入地图

系统初始化已预置5幅小型地图可供使用，平台暂不支持自动导入地图。

如需接入其它地图，需后台手动对接，具体请联系我司商务人员。

# 动态场景描述

当前系统场景交通流可通过动态场景描述Scenest进行描述，当前Scenest语言需要与地图关联，请注意已通过语言脚本中备注说明。

## Scenest场景描述语言介绍

### *scenest语言中的场景由以下几个部分组成:*

### 1. 场景（scenario）

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

### 3. 控制车辆（ego vehicle）

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

### 4. NPC车辆（NPC vehicles）

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

### 5. 行人（pedestrians）

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

### 6. 障碍物(obstacles)

你可以设置多个`障碍物（obstacle）`，每个障碍物由关键字`Obstacle`指定，并由`位置（position），形状（shape）`组成

6.1 形状（shape）

形状只有预设的形状：`球（sphere），立方体（box），圆锥（cone），圆柱（cylinder）`

```text
position=(1,2);
box_shape=(box,1,1,1);//表示一个立方体障碍物，长宽高为1,1,1
obstacle1=Obstacle(position,box_shape);//构造一个障碍物
obstacles={obstacle1,obstacle2};//表示多个障碍物
```

### 7. 环境（environment）

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

### 8. 交通（traffic）

交通由车道`交汇路口交通情况（intersection traffic）`与`车道限速（speed limitation）`组成。交汇路口的交通情况可以指定交汇路口的`交通灯（traffic light），停止信号（stop sign），人行横道（crosswalk）`格式如下：`Intersection(intersection id,traffic light,stop sign,crosswalk)`车道（lane）的限速情况：`SpeedLimit(lane id,(speed-min,speed-max)`

```text
intersection1=Intersection(3,0,0,0);
intersection2=Intersection(6,1,1,0);
speedlimit1=(1,(80,120));//表示车道1的限速情况
traffic={intersection1,intersection2,speedlimt1};
```

### 其它

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


## Scenest断言描述介绍

### *scenest语言中的断言由以下几个部分组成:*

### 1 规划路径（Trace） 

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

### 2 断言（Assertion）

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

### 3. 断言附加到规划路径上

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



# 近期目标

1 优化操作逻辑，车辆动力学模型、传感器模型 可独立车辆单独创建。

2 车辆动力学模型与轮胎动力学模型数据结构合并。

3 支持OpenScenrio 1.0格式场景描述语言。

***
