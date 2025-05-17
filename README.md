<p align="center"><strong>robot_descriptions</strong></p>
<p align="center"><a href="https://github.com/${YOUR_GIT_REPOSITORY}/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-orange"/></a>
<img alt="language" src="https://img.shields.io/badge/language-c++-red"/>
<img alt="platform" src="https://img.shields.io/badge/platform-linux-l"/>
</p>
<p align="center">
    语言：<a href="./docs/docs_en/README_EN.md"><strong>English</strong></a> / <strong>中文</strong>
</p>

机器人描述文件，目前包含`tita`以及其他四轮足机器人。文件夹命名结构为`{机器人名称}_description`。`robot_description`中的`xml`包含所有机器人描述文件。

### 构成
- `config`：rviz配置文件，默认不修改
- `launch`：启动rviz可视化和joint_state_publisher
- `meshes`：机器人模型文件，
- `urdf`：机器人URDF文件, 最原始导出的urdf文件
- `xacro`: 主要包含`meterials`，`ros2control`，以及整体描述机器人的`robot.xacro`

### 添加你的机器人
以下以`tita_description`为例，介绍如何添加新的机器人描述文件。例如你新增加的机器人名称为`rr`，则需要按照以下步骤进行：
- 复制`tita_description`，重命名为`rr_description`。, 搜索新复制的文件夹内所有`tita`字符或前缀，改为为你的机器人名称`rr`。
- 替换`meshes`文件夹下为你`rr`的机器人模型文件，替换`urdf`文件夹下的`urdf`为你的`urdf`文件。
- 将`xacro`文件夹下`robot.xacro`，第10-288行替换为你的`urdf`文件夹下的`urdf`中从`<link name="base_link">`到倒数第二行。
- 将`xacro`文件夹下`ros2control.xacro`中有关`<joint name="`后面的名称改成你的urdf中对应的`joint`名称。如果关节多则删除，少则添加。

- 
```bash
# 以编译tita_description为例
colcon build --packages-up-to tita_description
soure install/setup.bash
ros2 launch tita_description display.launch.py
```

