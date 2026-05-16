# 这是什么？

这是2025赛季的用于仿真测试的px4源码，版本号为1.15.4。创建这一仓库的原因是，px4版本更新很快，各种模块和依赖在一年后的新版本中很有可能无法使用，于是留存这一曾经顺利运行过的仿真源码。针对仿真的主要修改集中在 [gz 子仓库](https://github.com/kongpincheng1/gz-custom)。

## firmware 子模块

本仓库还包含 [firmware](https://github.com/kongpincheng1/Firmware1_15_4) 子模块，提供以下飞控的预编译固件：
- **雷迅 CUAV X7+**：`firmware/cuav_x7pro_default.px4`
- **雷迅 CUAV V6X**：`firmware/px4_fmu-v6x_default.px4`

这些固件均为 PX4 v1.15.4 版本，可直接用于实机烧录。

# 你该怎么做
你可以在px4官网找到完整安装[教程](https://docs.px4.io/main/en/dev_setup/dev_env_linux_ubuntu)

## 1.克隆仓库
```bash
git clone --recurse-submodules https://github.com/kongpincheng1/PX4-1.15.4-2025_Season.git
```
这一步耗时较久

## 2.安装依赖
进入仓库根目录后

```bash
bash ./Tools/setup/ubuntu.sh
```

如果你仅需要仿真，可以在命令后加--no-nuttx（这主要用于实机飞行）
即
```bash
bash ./Tools/setup/ubuntu.sh --no-nuttx
```

如果你不需要仿真，可以在命令后加--no-sim-tools
即
```bash
bash ./Tools/setup/ubuntu.sh --no-sim-tools
```

## 3.完成后重启电脑。

## 4.安装通信代理

此处[教程](https://docs.px4.io/main/en/ros2/user_guide)对应

```bash
git clone -b v3.0.1 https://github.com/eProsima/Micro-XRCE-DDS-Agent.git
cd Micro-XRCE-DDS-Agent
mkdir build
cd build
cmake ..
make
sudo make install
sudo ldconfig /usr/local/lib/
```
## 5.启动仿真

在仓库根目录下运行
```bash
make px4_sitl
make px4_sitl gz_x500_depth
```
若显示无可执行的文件，上网查找解决方案

## 6.连接仿真和程序

```bash
MicroXRCEAgent udp4 -p 8888
```
## 7.安装gz_bridge
```bash
sudo apt remove ros-humble-ros-gz
sudo apt install ros-humble-ros-gzgarden
```

助顺利

---
