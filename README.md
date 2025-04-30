# vlm_demo 视觉语言大模型

## 1. 功能介绍

`vlm_demo` 是在地瓜机器人 RDK 平台上在线调用大模型的通用型案例，用户可在 RDK 平台上也可在自己的 PC 机上在线体验 VLM 的强大功能。不论是在自己的 PC 机还是在 RDK 平台上，目前提供两种体验方式：
- 直接在终端输入文本与大模型进行自然对话；
- 或者是采用麦克风直接与大模型进行人机交互。

## 2. 物料清单

该系统可在以下平台上运行：
- RDK X3（4GB 内存）
- RDK Ultra
- PC 机（测试过 Ubuntu 18.04、20.04 和 22.04 的系统均无问题）
- USB 接口的麦克风（经测试有线耳机、蓝牙耳机均可）

## 3. 使用方法

### 3.1 准备工作

- 确认地瓜机器人 RDK X3 为 4GB 内存版本；
- 地瓜机器人 RDK X3 和 RDK Ultra 已烧录好地瓜机器人提供的 Ubuntu 20.04 系统镜像；
- 采用在线调用百度千帆和零一万物大模型。需要在对应官网上申请属于自己的 API Key，然后在 `vlm_demo` 中的 `API_KEY.py` 文件中替换成自己的 Key，方法参见官方文档说明：
  - [百度千帆](https://qianfan.cloud.baidu.com)
  - [零一万物](https://www.lingyiwanwu.com)

### 3.2 配置相关环境

以下是在 RDK 平台上配置的详细步骤，PC 机上的配置流程基本一致：

- 需要有 Python 3.9 环境。推荐使用 Miniforge，安装过程可参考 CSDN 中 Yabooo0 的文章：《Ubuntu 中安装 Miniforge》。使用 `conda` 创建一个新的环境用于配置大语言程序：
  ```bash
  conda create -n vlm python=3.9

- 如果使用lcm通信，那么安装lcm-1.3.1
  ```bash
  sudo apt-get install open-8-jdk
  # 进入lcm文件夹
  ./configure
  # 确保jave support 打开，然后
  make
  sudo make install
  sudo ldconfig

- 然后激活创建的conda环境
  ```bash
  conda activate vlm

- 开始配置大语言程序的环境（可以直接运行vlm_demo文件夹中的doggy.py程序看看缺少什么功能包，直接安装即可）
  ```bash
  # 安装依赖项
  sudo apt-get install libasound-dev portaudio19-dev libportaudio2 libportaudiocpp0
  pip install pyaudio
  pip install pyalsaaudio
  pip install numpy==1.16.4
  # cv_bridge报错修复numpy即可
  pip install pydub
  pip install appbuilder-sdk
  pip install qianfan
  pip install openai
  pip install lcm
  pip install rospkg
  pip insyall catkin-tools
  pip install opencv-python
  pip install pillow
  # roscore报错libroscppp.so 时，输入
  sudo setcap -r /usr/bin/python3.8（每次重新开机都要输入）

- 安装ROS
  ```bash
  # 按照国内鱼香肉丝一键安装ROS教程进行安装
  wget http://fishros.com/install -O fishros && . fishros

### 3.3 程序运行

- 启动 ROS 环境
  ```bash
  roscore
- 启动大模型程序
  ```bash
  python vlm_demo/doggy.py

### 3.4 效果展示
本项目效果展示见哔哩哔哩视频：https://www.bilibili.com/video/BV1HsexeHETX/?spm_id_from=333.999.0.0&vd_source=4bfff5ac9a1ffa49a122fe82b1f1d682

## 4. 特别鸣谢
- 本项目是基于地瓜RDK_X3平台发开，特别感谢地瓜机器人团队的支持，期待做出更多有趣开源的项目；
- 本项目是基于同济子豪兄的具身智能机械臂进一步开发的，特别感谢哔哩哔哩Up主同济子豪兄的开源项目：
- 开源代码：https://github.com/TommyZihao/vlm_arm
- 亚马逊云科技生成式AI平台Amazon Bedrock：https://aws.amazon.com/cn/bedrock
- 哔哩哔哩视频：https://www.bilibili.com/video/BV1Cn4y1R7V2/?spm_id_from=333.337.search-card.all.click&vd_source=4bfff5ac9a1ffa49a122fe82b1f1d682

 ---