# SpharxTools - 数据智能基础设施工具集

<div align="center">

[![License](https://img.shields.io/badge/license-GPL3.0-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.10%2B-blue.svg)](https://www.python.org/)
[![Docker](https://img.shields.io/badge/docker-ready-green.svg)](https://www.docker.com/)
[![Platform](https://img.shields.io/badge/platform-Linux%20%7C%20Windows-lightgrey.svg)](#)

**人工智能时代的物理世界数据处理工具集**
-

<h4>"From data intelligence emerges"<h4>
<h4>"始于数据，终于智能"<h4>

</div>

## 🎯 项目简介

SpharxTools 是 SPHARX 极光感知科技的核心工具集，专注于物理世界数据的采集、预处理和深度加工。作为 SpharxWorks 数据智能基础设施的重要组成部分，SpharxTools 提供了从原始传感器数据到高价值数据资产的完整处理链路。

**核心组件**:
- **Workshop**: 物理世界数据工厂，负责数据采集与预处理
- **Deepness**: 深度加工生产线，负责数据语义化和物理属性预测

---

## 🏭 目录结构

```
SpharxTools/
├── Workshop/              # 物理世界数据工厂
│   ├── common/            # 通用组件
│   ├── commons/           # 公共工具
│   ├── hardware/          # 硬件抽象层
│   ├── pipelines/         # 六阶段处理流水线
│   │   ├── run_00_ingest/     # 数据导入
│   │   ├── run_01_quality/    # 质量检测
│   │   ├── run_02_enhance/    # 数据增强
│   │   ├── run_03_calibrate/  # 相机标定
│   │   ├── run_04_pack/       # 数据打包
│   │   └── run_05_delivery/   # 数据交付
│   ├── scripts/           # 工具脚本
│   ├── tests/             # 测试套件
│   └── workshop/          # 核心框架
├── Deepness/              # 深度加工生产线
│   ├── deepness/          # 核心代码
│   │   ├── core/              # 核心组件
│   │   ├── orchestration/     # 编排系统
│   │   └── pipelines/         # 四大处理管道
│   │       ├── run_01_spatial_prior/     # 空间先验生成
│   │       ├── run_02_physics_jepa/      # 物理属性预测
│   │       ├── run_03_causal_trajectory/ # 交互轨迹记录
│   │       └── run_04_benchmark_export/  # 评测数据导出
│   ├── docs/              # 文档
│   ├── scripts/           # 部署和构建脚本
│   └── tests/             # 测试套件
└── README.md              # 项目说明文档
```

---

## 🔧 1. Workshop - 物理世界数据工厂 ✅ 生产就绪 (v1.0.3.7)

Workshop 是 SpharxTools 的数据采集与预处理核心平台，采用模块化、容器化的架构设计，实现了从原始传感器数据到标准化高质量数据集的完整处理链路。

### 🔄 六阶段处理流水线

```
原始数据输入 
→ 00_ingest (数据导入) 
→ 01_quality (质量检测) 
→ 02_enhance (数据增强) 
→ 03_calibrate (相机标定) 
→ 04_pack (数据打包) 
→ 05_delivery (数据交付) 
→ 标准化数据集
```

### 🧩 核心模块详解

#### 00_ingest - 数据导入模块
- **功能职责**：接收和解析原始传感器数据，实现隐私脱敏处理
- **技术栈**：Intel RealSense SDK、OpenCV、ROS Bag 解析
- **输入格式**：ROS Bag 文件、RealSense 数据流
- **输出结构**：标准化目录结构（rgb/、depth/、calibration/、timestamps.csv等）
- **关键技术**：实时数据流处理、隐私保护算法

#### 01_quality - 质量检测模块
- **功能职责**：多层次数据质量评估与验证
- **检测维度**：硬件层（模糊度、曝光、帧率）、语义层（动作完整性）
- **输出产物**：quality_report.json、详细质量指标数据
- **配置灵活性**：可调节的质量阈值和检测参数

#### 02_enhance - 数据增强模块
- **功能职责**：基于目标检测的数据增强和自动标注
- **核心技术**：YOLOv8 实时目标检测、图像去噪算法
- **输出格式**：COCO 格式标注文件、增强后的图像数据
- **模型支持**：yolov8n.pt（可替换为其他 YOLOv8 模型）

#### 03_calibrate - 相机标定模块
- **功能职责**：相机内外参精确标定
- **标定方法**：棋盘格标定法、标定精度验证
- **输出内容**：内参矩阵、外参矩阵、详细标定报告
- **支持范围**：单相机内参标定（外参标定预留）

#### 04_pack - 数据打包模块
- **功能职责**：标准化数据集打包与完整性校验
- **支持格式**：ROS Bag 格式、COCO 格式、自定义扩展格式
- **质量保证**：自动完整性检查、SHA256 校验和生成
- **验证机制**：格式验证和数据一致性检查

#### 05_delivery - 数据交付模块
- **功能职责**：数据集上传和交付管理
- **交付方式**：阿里云 OSS 对象存储、SFTP 安全传输、本地存储
- **可靠性保障**：重试机制、交付状态通知、完整性验证

### 🛠️ 技术架构

**基础设施**：
- **容器化**：基于 Docker 的微服务架构，支持弹性扩展
- **编程语言**：Python 3.10+，核心框架包括 OpenCV、PyTorch、YOLOv8
- **硬件支持**：Intel RealSense SDK，支持多种传感器设备
- **配置管理**：YAML 格式统一配置，环境变量灵活控制

**工程实践**：
- **配置驱动**：模块化配置管理体系，支持热更新
- **监控可观**：完善的日志系统和实时状态监控
- **安全合规**：容器安全策略和数据保护机制
- **持续集成**：自动化测试和部署流水线

### 📈 当前应用状况

Workshop v1.0.3.7 版本已达到生产就绪状态，在实际项目中稳定运行：
- ✅ 完成硬件同步方案（3×D455 相机）
- ✅ 实现 RealSense 数据解析功能
- ✅ 集成 YOLOv8 目标检测
- ✅ 建立完整的质量控制体系
- ✅ 支持多种数据交付方式
- ✅ 六阶段流水线全部模块生产就绪

### 🚀 快速开始

```bash
# 克隆项目
cd /home/spharx/SpharxWorks/SpharxTools/Workshop

# 安装依赖
pip install -r requirements.txt

# 运行完整流水线
bash scripts/pipeline/run_full.sh --input /path/to/input --output /path/to/output

# 运行单模块测试
bash scripts/test/run_tests.sh
```

**文档**: [Workshop 完整文档](Workshop/README.md) | [架构设计](Workshop/docs/WORKSHOP_ARCH.md)

---

## ⚡ 2. Deepness - 深度加工生产线 ⚡ 开发中 (v1.0.4.0)

Deepness 是 SpharxTools 的核心深度加工子系统，致力于将原始物理世界数据转化为富含语义和物理属性的高价值数据资产。

### 🔄 四大核心处理管道

#### 01_spatial_prior - 空间先验生成管道
- **技术基础**: 基于 NVIDIA Cosmos 世界模型实现空间理解
- **核心功能**: 生成场景的语义分割和几何先验
- **输出产物**: 语义地图、几何先验、Cosmos 特征向量
- **技术栈**: PyTorch 2.5.1 (CUDA 12.1)、NVIDIA Cosmos

#### 02_physics_jepa - 物理属性预测管道
- **技术基础**: 基于 Meta JEPA 架构预测物体物理属性
- **核心功能**: 推断材质、密度、摩擦系数等参数
- **输出产物**: 标准化 3D 网格模型、物理属性元数据
- **技术栈**: PyTorch 2.5.1、PyTorch3D 0.7.6、Open3D 0.18.0

#### 03_causal_trajectory - 交互轨迹记录管道
- **技术组成**: 整合多模态感知数据（RGB-D + IMU）
- **核心能力**: 记录物理交互轨迹和行为模式
- **高级功能**: 支持反事实推演和仿真验证
- **技术支撑**: YOLOv8 目标检测、ORB-SLAM3/LIO-SAM 定位、PyBullet 物理仿真

#### 04_benchmark_export - 评测数据导出管道
- **转换能力**: 支持多种标准评测格式
- **兼容框架**: Genie Sim 3.0、NVIDIA Cosmos、Meta JEPA 等主流框架
- **质量保障**: 提供数据质量报告和完整性验证
- **扩展支持**: 可定制的导出适配器

### 📊 技术架构详情

**基础设施**:
- **Docker 容器化**: 基于 CUDA 12.1 的 Ubuntu 22.04 基础镜像
- **Python 环境**: Miniforge3 + Python 3.11，预装科学计算包
- **深度学习**: PyTorch 2.5.1 (CUDA 12.1)、PyTorch3D 0.7.6
- **3D 处理**: Open3D 0.18.0、Kaolin 0.17.0、gsplat 渲染引擎
- **世界模型**: NVIDIA Cosmos、Meta JEPA
- **视觉算法**: YOLOv8、ORB-SLAM3、LIO-SAM

**配置管理**:
- **统一配置中心**: YAML 格式，支持模块化配置
- **环境变量控制**: 通过 .env 文件管理运行参数
- **版本锁定**: deps.lock 文件确保依赖一致性

### 📈 开发进度与规划

当前版本 v1.0.4.0 开发进度 80%:
- ✅ 基础架构搭建完成
- ✅ Docker 容器化配置就绪
- ✅ 四个核心处理模块全部实现
  - ✅ run_01_spatial_prior (Cosmos 适配器)
  - ✅ run_02_physics_jepa (JEPA 物理预测)
  - ✅ run_03_causal_trajectory (SLAM+ 因果推理)
  - ✅ run_04_benchmark_export (多格式导出)
- ⏳ 端到端集成测试中 (80%)
- 🔲 性能基准测试

### 🚀 快速开始

```bash
# 克隆项目
cd /home/spharx/SpharxWorks/SpharxTools/Deepness

# 下载依赖和模型
bash scripts/download/download_deps.sh
bash scripts/download/download_models.sh

# 构建和运行
bash scripts/build/deepness_build_all.sh
bash scripts/deploy/deepness_deploy.sh

# 测试
bash scripts/test/run_tests.sh
```

**文档**: [Deepness 技术文档](Deepness/README.md) | [管道详解](Deepness/docs/README_pipelines.md)

---

## 🔧 技术栈

| 类别 | 技术/框架 | 版本 | 用途 |
|------|-----------|------|------|
| **编程语言** | Python | 3.10+ | 核心开发语言 |
| **深度学习** | PyTorch | 2.5.1 | 神经网络训练和推理 |
| **计算机视觉** | OpenCV | 4.8.0+ | 图像处理和计算机视觉 |
| **3D 处理** | Open3D | 0.18.0 | 3D 点云处理 |
| **目标检测** | YOLOv8 | 8.0.20 | 实时目标检测 |
| **硬件接口** | Intel RealSense SDK | 2.54.1 | 相机数据采集 |
| **容器化** | Docker | 20.10+ | 环境隔离和部署 |
| **配置管理** | YAML | - | 配置文件格式 |
| **世界模型** | NVIDIA Cosmos | - | 空间理解 |
| **世界模型** | Meta JEPA | - | 物理属性预测 |
| **SLAM** | ORB-SLAM3 | - | 视觉定位 |
| **SLAM** | LIO-SAM | - | 激光惯性定位 |
| **物理仿真** | PyBullet | 3.2.5 | 物理模拟 |

---

## 📈 发展路线图

### 短期目标 (2026 Q2-Q3)
- ✅ **Workshop v1.0.3.7** 生产就绪 - 六阶段流水线全部模块完成
- ⏳ **Deepness v1.0.4.0** 端到端集成 (80%) - 四大处理管道联调中

### 中期规划 (2026 Q4-2027)
- 🚀 **Deepness v1.1.0** 正式发布 - 完成性能基准测试和生产部署
- 🔄 **Workshop → Deepness 完整数据流** - 实现两个系统的无缝集成
- 🌐 **开发者生态** - Python SDK 完善和示例丰富

### 长期愿景 (2027+)
- 🌐 **物理 AI 基础设施** - 成为人工智能时代的物理世界数据处理标准
- 🤝 **全球化开源社区** - 建立开放包容的技术生态
- 🏆 **下一代技术引领** - 物理世界理解与智能决策技术的持续创新

---

## 🤝 生态合作

我们诚邀各界合作伙伴共同建设物理世界数据处理生态：

### 技术合作伙伴
- **硬件厂商**：传感器、相机、GPU/NPU计算设备提供商
- **算法团队**：3D 重建、SLAM、物理仿真、大模型等领域专家
- **应用企业**：机器人、自动驾驶、AR/VR、智能助理等落地场景

### 社区贡献
- **代码贡献**：核心功能开发和优化
- **文档完善**：使用指南和技术文档
- **测试验证**：功能测试和性能评估
- **生态建设**：社区运营和知识分享

---

## 📧 联系方式

### 统一联系邮箱
- **技术支持**：lidecheng@spharx.cn（Workshop / Deepness）
- **安全问题**：wangliren@spharx.cn（安全漏洞报告）
- **商务合作**：zhouzhixian@spharx.cn

### 官方网站
- **主站**：https://spharx.cn
- **Gitee 仓库**：https://gitee.com/spharx
- **GitHub 镜像**：https://github.com/SpharxTeam

## 📚 技术资源

### 核心文档
- [📘 **Workshop 完整文档**](Workshop/README.md) - 数据工厂详细说明
- [🔬 **Deepness 技术文档**](Deepness/README.md) - 深度加工技术细节

### 架构设计
- [🏗️ **Workshop 架构文档**](Workshop/docs/WORKSHOP_ARCH.md) - 详细架构设计
- [🔬 **Deepness 管道文档**](Deepness/docs/README_pipelines.md) - 处理管道详细说明

### 开发资源
- [📋 **编码规范**](Workshop/docs/CODING_STANDARDS.md) - 开发标准和规范
- [🧪 **测试指南**](Workshop/tests/docs/TESTING_GUIDE.md) - 测试框架说明
- [📈 **项目进度**](Workshop/docs/PROGRESS.md) - 开发里程碑跟踪

---

## 📄 许可证与授权

SpharxTools 采用 **GPL-3.0 开源协议 + 商业闭源授权** 双授权模式，您可根据自身使用场景选择对应授权。

### 开源授权（GPL-3.0）
个人学习、学术研究、非商业原型验证、开源社区贡献等非商业场景，可免费使用本项目，需严格遵守 GPL-3.0 协议的开源义务，完整协议详见 [LICENSE-GPL-3.0](LICENSE-GPL-3.0)。

### 商业闭源授权
任何将本项目用于闭源商业产品、商业服务、盈利性项目的行为，均需提前向 SPHARX 极光感知科技申请商业授权，获得闭源使用豁免、官方技术支持、定制化服务等权益。

商业授权详情详见 [LICENSE-COMMERCIAL](LICENSE-COMMERCIAL)，授权申请请联系：
- 官方邮箱：lidecheng@spharx.cn、wangliren@spharx.cn
- 官方网站：https://spharx.cn

---

## 🙏 致谢

感谢所有为开源社区做出贡献的开发者们，正是你们的努力让这样的项目成为可能。



<div align="center">

<h3>From data intelligence emerges</h3>
<h3>始于数据，终于智能</h3>

<p><em>构建 AI 时代的物理世界数据处理工具集</em></p>

#### 📞 联系我们

📧 邮箱：lidecheng@spharx.cn & wangliren@spharx.cn

<p>
  <a href="https://github.com/spharx">GitHub</a> ·
  <a href="https://gitee.com/SpharxTeam">Gitee</a> ·
  <a href="https://spharx.cn">官方网站</a> ·
  <a href="mailto:lidecheng@spharx.cn">技术支持</a>
</p>

© 2026 SPHARX Ltd. All Rights Reserved.

</div>