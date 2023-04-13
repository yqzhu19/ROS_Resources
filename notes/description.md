##### 机器人描述description
- 文件 urdf
- urdf语法规范：XML specifications
- 【https://zhuanlan.zhihu.com/p/452791019】


- 2.1 robot：根标签，所有的link和joint以及其他标签都必须在robot标签内。在该标签内用过name属性设置机器人模型的名称。
- 2.2 link: 用于描述机器人(也即刚体部分)某个部件的外观和物理属性，每一个部件对应一个link。在link内，可以设计该部件的形状，尺寸，颜色，惯性矩阵，碰撞参数等一系列属性。link标签中主要包含3个子标签，visual，collision，inertial。
  - visual: 用于描述外观
    - geometry: 设置连杆的形状
    - origin: 设置连杆的偏移量与倾斜弧度
    - metrial: 设置连杆的材料属性(颜色)
  - collision: 用于设置连杆的碰撞属性。提供碰撞检测的依据。
    - 对于简单的几何图形，直接复制粘贴visual标签下的geometry和origin两个子标签的设置即可，
  - inertial: 用于设置连杆的惯性矩阵。inertial 标签标注了当前机器人某个刚体部分的惯性矩阵，用于一些力学相关的仿真计算。其下也有三个子标签，分别为origin、mass、inertia。
- 2.3 joint: 用于描述机器人关节的运动学和动力学属性。joint标签自身有两个属性name，type可以设置，使用name为关节命名，使用type指定关节的运动形式。joint标签描述2个link之间的关系。
  - ![image](https://user-images.githubusercontent.com/44147850/231896310-3fed07d6-72e1-462e-a863-a7a82f90fbf4.png)
- 2.4 其他
  - gazebo标签：如果想在gazebo中重现模型，需要重新使用 gazebo 标签标注颜色。（之前的颜色设置在gezebo仿真环境下无效。）关于在gazebo中仿真的更多说明见后文。



#### 二、Xacro语法
##### 1. xacro提高urdf的复用性
##### 2. 具体语法
- 2.1 根标签robot
- name = ‘你定义的名字’
- xmlns:xacro=“http://wiki.ros.org/xcaro”
- <robot xxxxxxx >
- </robot> 结束
- 2.3 宏（类函数）
- 宏的定义与调用，与C语言中的函数定义与调用相似。
- 宏的定义：
- <xacro:macro name="你定义的名字" params="参数列表，多参数之间使用空格分隔" >
- </xacro:macro>
- 宏的调用：
- <xacro:宏名称 参数1=xxx 参数2=xxx>
- 2.4 文件包含：
- 机器人模型由多部件组成，不同部件可封装为单独的xcaro文件，最后再将不同的文件集成，组成完整的机器人。

'''
  <robot  name="你定义的名字" xmlns:xacro="http://wiki.ros.org/xacro">
    <xacro:include filename="demo05_car_base.xacro" />
    <xacro:include filenmae="demo06_car_camera.xacro" />
    <xacro:include filename="demo07_car_laser.xacro" />
  </robot>
 '''

- 3. launch中加载:
- 编写玩xacro文件后，想在launch文件中加载，有两种方式可选。
- 1. xacro -> urdf -> 集成urdf文件 -> 在launch文件中加载
- 2. 直接在launch文件中以xacro形式加载。
