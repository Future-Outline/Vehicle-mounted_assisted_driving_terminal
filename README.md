# 智能车载终端系统


## 📋 项目概述

智能车载终端系统是基于RK3588 ELF2开发板构建的嵌入式AI系统，集成了摄像头、毫米波雷达和AI推理引擎，为智能驾驶提供实时环境感知和决策支持。

### 🎯 核心功能

- **实时图像处理**：OV13855摄像头采集，OpenCV实时处理
- **AI目标检测**：YOLO模型 + RKNN加速，车辆/行人识别
- **距离测量**：HLK-LD2451毫米波雷达，精确距离检测
- **多传感器融合**：摄像头与雷达数据融合分析
- **用户界面**：实时显示检测结果和距离信息

## 🏗️ 系统架构

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   摄像头模块     │    │   雷达模块       │    │   AI推理模块     │
│   OV13855       │    │  HLK-LD2451     │    │  YOLO + RKNN    │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         └───────────────────────┼───────────────────────┘
                                 │
                    ┌─────────────────┐
                    │   数据融合模块   │
                    │   Sensor Fusion │
                    └─────────────────┘
                                 │
                    ┌─────────────────┐
                    │   用户界面模块   │
                    │   GUI Display   │
                    └─────────────────┘
```

## 🛠️ 技术栈

### 硬件平台
- **主控芯片**：RK3588 ARM Cortex-A76
- **摄像头**：OV13855 13MP图像传感器
- **雷达**：HLK-LD2451 24GHz毫米波雷达
- **存储**：eMMC + SD卡扩展
- **接口**：USB3.0、UART、I2C、SPI

### 软件环境
- **操作系统**：Linux (RK3588)
- **编程语言**：Python 3.8~3.10.5
- **AI框架**：RKNN-Toolkit2
- **图像处理**：OpenCV 4.x
- **深度学习**：YOLO11n
- **打包工具**：PyInstaller

## 📦 安装部署

### 环境要求
- RK3588 ELF2开发板
- Linux系统 (Ubuntu 20.04+)
- Python 3.8~3.10.5
- 至少4GB RAM
- 至少16GB存储空间

### 依赖安装

```bash
# 更新系统包
sudo apt update && sudo apt upgrade -y

# 安装Python依赖
pip install -r requirements.txt

# 安装RKNN-Toolkit2 (需要从官方获取)
# 请参考RKNN官方文档进行安装
```

### 快速部署

```bash
# 克隆项目
git clone https://github.com/your-username/smart-vehicle-terminal.git
cd smart-vehicle-terminal

# 安装依赖
pip install -r requirements.txt

# 运行程序
python main.py

# 打包部署
python build.py
```

## 🚀 使用方法

### 启动方式

#### 1. 命令行启动
```bash
cd /path/to/project
python main.py
```

#### 2. 桌面图标启动
双击桌面上的"智能车载系统"图标（由于文件过大本次上传并非打包应用版，如有需要请联系我们）

#### 3. 脚本启动
```bash
./start_system.sh
```

### 操作界面

启动后系统会显示以下界面：
- **实时视频窗口**：显示摄像头采集的画面
- **检测结果窗口**：显示YOLO检测结果
- **距离信息面板**：显示雷达测距数据
- **控制面板**：系统参数调节

### 功能操作

1. **图像检测**：自动识别车辆、行人等目标
2. **距离测量**：实时显示目标距离信息
3. **数据记录**：自动保存检测日志
4. **参数调节**：实时调整检测阈值

## 📊 性能指标

| 指标 | 数值 | 说明 |
|------|------|------|
| 检测精度 | >95% | YOLO模型在车辆数据集上的表现 |
| 检测延迟 | <50ms | 从图像采集到结果输出的时间 |
| 测距精度 | ±0.2m | 雷达在10m范围内的精度 |
| 测距范围 | 0.5-50m | 雷达有效检测范围 |
| 帧率 | 60fps | 实时视频处理帧率 |
| 功耗 | <5W | 系统整体功耗 |

## 🔧 开发指南

### 项目结构
```
smart-vehicle-terminal/
├── main.py                 # 主程序入口
├── camera/                 # 摄像头模块
│   ├── camera_manager.py   # 摄像头管理
│   └── image_processor.py  # 图像处理
├── radar/                  # 雷达模块
│   ├── radar_manager.py    # 雷达管理
│   └── distance_calc.py    # 距离计算
├── ai/                     # AI推理模块
│   ├── yolo_detector.py    # YOLO检测器
│   └── rknn_engine.py      # RKNN推理引擎
├── fusion/                 # 数据融合模块
│   └── sensor_fusion.py    # 传感器融合
├── gui/                    # 用户界面模块
│   ├── main_window.py      # 主窗口
│   └── display_widgets.py  # 显示组件
├── utils/                  # 工具模块
│   ├── config.py           # 配置管理
│   └── logger.py           # 日志管理
├── models/                 # 模型文件
│   └── yolo_model.rknn     # RKNN模型
├── scripts/                # 脚本文件
│   ├── build.py            # 打包脚本
│   └── start_system.sh     # 启动脚本
└── docs/                   # 文档
    └── README.md           # 项目文档
```

### 核心模块说明

#### 摄像头模块 (`camera/`)
- 负责OV13855摄像头的初始化和图像采集
- 提供实时视频流和图像预处理功能
- 支持多种分辨率和帧率设置

#### 雷达模块 (`radar/`)
- 管理HLK-LD2451毫米波雷达
- 解析雷达数据包，计算目标距离
- 提供距离滤波和噪声抑制

#### AI推理模块 (`ai/`)
- 集成YOLO目标检测模型
- 使用RKNN-Toolkit2进行硬件加速
- 支持实时目标检测和分类

#### 数据融合模块 (`fusion/`)
- 融合摄像头和雷达数据
- 实现多传感器数据同步
- 提供综合环境感知信息

## 🐛 故障排除

### 常见问题

#### 1. 程序启动失败
```bash
# 检查Python环境
python --version

# 检查依赖安装
pip list | grep opencv
pip list | grep rknn

# 检查硬件连接
ls /dev/video*  # 检查摄像头
ls /dev/ttyUSB* # 检查雷达串口
```

#### 2. 摄像头无法识别
```bash
# 检查摄像头驱动
v4l2-ctl --list-devices

# 测试摄像头
ffmpeg -f v4l2 -i /dev/video0 -t 5 test.mp4
```

#### 3. 雷达通信失败
```bash
# 检查串口权限
sudo chmod 666 /dev/ttyUSB0

# 测试串口通信
minicom -D /dev/ttyUSB0 -b 115200
```

#### 4. AI推理速度慢
- 检查RKNN模型是否正确加载
- 确认RKNN-Toolkit2版本兼容性
- 优化模型输入尺寸

### 日志查看
```bash
# 查看系统日志
tail -f /var/log/syslog

# 查看程序日志
tail -f logs/system.log
```

## 📈 性能优化

### 系统优化建议

1. **内存优化**
   - 使用内存池管理图像缓存
   - 及时释放不需要的资源

2. **CPU优化**
   - 使用多线程处理不同模块
   - 优化图像处理算法

3. **GPU优化**
   - 充分利用RK3588 NPU
   - 优化RKNN模型推理

4. **存储优化**
   - 使用SSD提升I/O性能
   - 定期清理日志文件

## 🤝 贡献指南

欢迎提交Issue和Pull Request来改进项目！

### 开发流程
1. Fork项目到个人仓库
2. 创建功能分支 (`git checkout -b feature/xxx`)
3. 提交更改 (`git commit -am 'Add feature'`)
4. 推送分支 (`git push origin feature/xxx`)
5. 创建Pull Request

### 代码规范
- 遵循PEP 8 Python代码规范
- 添加适当的注释和文档
- 编写单元测试
- 确保代码通过所有测试


## 🙏 致谢

感谢以下开源项目和工具的支持：
- [OpenCV](https://opencv.org/) - 计算机视觉库
- [YOLO](https://github.com/ultralytics/yolov5) - 目标检测模型
- [RKNN-Toolkit2](https://github.com/rockchip-linux/rknn-toolkit2) - AI推理加速
- [PyInstaller](https://pyinstaller.org/) - Python打包工具

---

**注意**：本项目仅供学习和研究使用，请勿用于商业用途。本系统仅为智能车载终端示例，不可作为实例作用与汽车上。 