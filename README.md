# SpharxTools - 数据智能基础设施工具集

> **人工智能时代的物理世界数据处理工具集**
>
> "From data intelligence emerges"
>
> "始于数据，终于智能"

## 🎯 项目简介

SpharxTools 是 SPHARX 极光感知科技的核心工具集，专注于物理世界数据的采集、预处理和深度加工。作为 SpharxWorks 数据智能基础设施的重要组成部分，SpharxTools 提供了从原始传感器数据到高价值数据资产的完整处理链路。

**核心组件**:
- **Workshop**: 物理世界数据工厂，负责数据采集与预处理
- **Deepness**: 深度加工生产线，负责数据语义化和物理属性预测

---

## 🏭 目录结构

```
SpharxTools/
├── Workshop/              # 物理世界数据工厂 (v3.0.0)
│   ├── workshop/          # ★ 核心代码包 V3.0（五层架构）
│   │   ├── core/          # 核心层（抽象、服务、安全、可观测性）
│   │   ├── orchestration/ # 编排层（调度器、任务队列、工作流引擎）
│   │   └── services/      # 服务层（网关、监控、导出）
│   ├── commons/           # 通用层（工具函数、数据模式）
│   ├── common/            # 向后兼容层 (V2.0)
│   ├── pipelines/         # 六阶段处理流水线
│   │   ├── run_00_ingest/     # 数据导入
│   │   ├── run_01_quality/    # 质量检测
│   │   ├── run_02_enhance/    # 数据增强
│   │   ├── run_03_calibrate/  # 相机标定
│   │   ├── run_04_pack/       # 数据打包
│   │   └── run_05_delivery/   # 数据交付
│   ├── hardware/          # 硬件抽象层
│   ├── scripts/           # 工具脚本
│   ├── tests/             # 测试套件
│   └── docs/              # 技术文档
├── Deepness/              # 深度加工生产线 (v2.0.0)
│   ├── deepness/          # 核心代码（四层架构）
│   │   ├── core/              # 核心抽象层
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

## 🔧 1. Workshop - 物理世界数据工厂 ✅ 生产就绪 (v3.0.0)

Workshop 是 SpharxTools 的数据采集与预处理核心平台，基于 **AgentOS 微内核架构** 和 **Deepness 模块化设计** 构建，采用 **五层架构**（Core → Commons → Orchestration → Services → Pipelines）。从原始传感器数据到标准化高质量数据集，实现完整处理链路。

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

| 阶段 | 模块 | 核心功能 |
|------|------|---------|
| 1 | **00_ingest** | ROS Bag 解析、图像压缩、隐私脱敏 |
| 2 | **01_quality** | 模糊检测、曝光分析、帧丢弃检测 |
| 3 | **02_enhance** | YOLO 目标检测、HDVS 分割 |
| 4 | **03_calibrate** | 棋盘格相机校准、重投影误差评估 |
| 5 | **04_pack** | 多格式数据集打包 (ROS/COCO/YOLO/VOC/KITTI) |
| 6 | **05_delivery** | OSS 上传、交付通知、完整性校验 |

### 🛠️ 技术架构

**五层架构**:

| 层级 | 组件 | 说明 |
|------|------|------|
| **Pipelines** | run_00 ~ run_05 | 六阶段处理流水线 |
| **Services** | Gateway · Monitor · Exporter | 服务层接口 |
| **Orchestration** | Scheduler · TaskQueue · WorkflowEngine | 任务编排 |
| **Commons** | Utils · Schemas · Decorators | 通用工具 |
| **Core** | Abstractions · Services · Security · Observability | 核心基础设施 |

**工程实践**:
- **生产级质量**: 100+ 错误码体系，输入验证覆盖率 99%
- **安全内生**: SQL/XSS 检测、路径遍历防护、审计日志
- **可观测性**: 分布式追踪、性能监控、健康检查
- **DevOps**: GitHub Actions CI/CD，Docker 多阶段构建

### 📈 当前应用状况

Workshop v3.0.0 版本已达到生产就绪状态：
- ✅ 五层架构重构完成（V3.0）
- ✅ 基于 BasePipeline ABC 的标准化管道框架
- ✅ 完成硬件同步方案（3×D455 相机）
- ✅ 实现 RealSense 数据解析功能
- ✅ 集成 YOLOv8 目标检测
- ✅ 建立完整的质量控制体系
- ✅ 支持多种数据交付方式

### 🚀 快速开始

```bash
# 克隆项目
cd SpharxTools/Workshop

# 配置环境变量
cp .env.template .env

# Docker 一键启动
docker-compose up -d

# 验证服务状态
docker-compose ps
```

**文档**: [Workshop 完整文档](Workshop/README.md) | [架构设计](Workshop/docs/WORKSHOP_ARCH.md) | [项目结构V3](Workshop/docs/PROJECT_STRUCTURE_V3.md) | [开发者指南](Workshop/docs/DEVELOPER_GUIDE.md)

---

## ⚡ 2. Deepness - 深度加工生产线 ⚡ 开发中 (v2.0.0)

Deepness 是 SpharxTools 的核心深度加工子系统，致力于将原始物理世界数据转化为富含语义和物理属性的高价值数据资产。

### 🔄 四大核心处理管道

| 管道 | 功能 | 技术基础 |
|------|------|---------|
| **01_spatial_prior** | 空间先验生成 | NVIDIA Cosmos 世界模型 |
| **02_physics_jepa** | 物理属性预测 | Meta JEPA 架构 |
| **03_causal_trajectory** | 交互轨迹记录 | YOLOv8 + ORB-SLAM3/LIO-SAM |
| **04_benchmark_export** | 评测数据导出 | Genie Sim 3.0、JEPA、Spatial |

### 📊 技术架构

**四层架构**:

| 层级 | 组件 | 说明 |
|------|------|------|
| **应用层** | 四大处理管道 | 具体业务逻辑 |
| **编排层** | TaskQueue · ResourceManager · Scheduler · WorkflowEngine | 任务调度与资源管理 |
| **处理层** | 管道基类 | 标准化处理接口 |
| **核心层** | Abstractions · Services · Security · Observability | 基础抽象 |

**技术栈**:
- **深度学习**: PyTorch 2.5.1 (CUDA 12.1)、PyTorch3D 0.7.6
- **3D 处理**: Open3D 0.18.0、Kaolin 0.17.0、gsplat 渲染引擎
- **世界模型**: NVIDIA Cosmos、Meta JEPA
- **视觉算法**: YOLOv8、ORB-SLAM3、LIO-SAM
- **物理仿真**: PyBullet

### 📈 开发进度

当前版本 v2.0.0 开发进度 90%:
- ✅ 基础架构搭建完成
- ✅ Docker 容器化配置就绪
- ✅ 四个核心处理模块全部实现
- ✅ 核心架构重构完成（四层架构、安全与可观测性层、统一包结构）
- ⏳ 端到端集成测试中 (90%)
- 🔲 性能基准测试

### 🚀 快速开始

```bash
# 克隆项目
cd SpharxTools/Deepness

# 下载依赖和模型
./scripts/download/download_deps.sh
./scripts/download/download_models.sh

# 构建系统
make all

# 启动服务
docker-compose up -d
```

**文档**: [Deepness 技术文档](Deepness/README.md) | [管道详解](Deepness/docs/README_pipelines.md) | [开发者指南](Deepness/docs/DEVELOPER_GUIDE.md)

---

## 📈 发展路线图

### 短期目标 (2026 Q2-Q3)
- ✅ **Workshop v3.0.0** 生产就绪 - 五层架构重构完成，六阶段流水线全部模块完成
- ⏳ **Deepness v2.0.0** 端到端集成 (90%) - 四大处理管道联调中

### 中期规划 (2026 Q4-2027)
- 🚀 **Deepness v2.3.0** 正式发布 - 完整流水线正式发布
- 🚀 **Workshop v3.1.0** - 性能优化和功能扩展
- 🔄 **Workshop → Deepness 完整数据流** - 实现两个系统的无缝集成
- 🌐 **开发者生态** - Python SDK 完善和示例丰富

### 长期愿景 (2027+)
- 🌐 **物理 AI 基础设施** - 成为人工智能时代的物理世界数据处理标准
- 🤝 **全球化开源社区** - 建立开放包容的技术生态
- 🏆 **下一代技术引领** - 物理世界理解与智能决策技术的持续创新

---

## 📧 联系方式

- **技术支持**: lidecheng@spharx.cn
- **安全问题**: wangliren@spharx.cn
- **商务合作**: zhouzhixian@spharx.cn

### 官方网站
- **主站**: https://spharx.cn
- **Gitee 仓库**: https://gitee.com/spharx
- **GitHub 镜像**: https://github.com/SpharxTeam

## 📚 技术资源

### 核心文档
- [Workshop 完整文档](Workshop/README.md) - 数据工厂详细说明
- [Deepness 技术文档](Deepness/README.md) - 深度加工技术细节

### 架构设计
- [Workshop 架构文档](Workshop/docs/WORKSHOP_ARCH.md) - 详细架构设计
- [Deepness 管道文档](Deepness/docs/README_pipelines.md) - 处理管道详细说明

### 开发资源
- [Workshop 编码规范](Workshop/docs/CODING_STANDARDS.md) - 开发标准和规范
- [Workshop 测试指南](Workshop/tests/docs/TESTING_GUIDE.md) - 测试框架说明
- [Workshop 项目进度](Workshop/docs/PROGRESS.md) - 开发里程碑跟踪

---

## 📄 许可证与授权

SpharxTools 采用 **GPL-3.0 开源协议 + 商业闭源授权** 双授权模式。

### 开源授权（GPL-3.0）
个人学习、学术研究、非商业原型验证、开源社区贡献等非商业场景，可免费使用本项目，需严格遵守 GPL-3.0 协议的开源义务。

### 商业闭源授权
任何将本项目用于闭源商业产品、商业服务、盈利性项目的行为，均需提前向 SPHARX 极光感知科技申请商业授权。

商业授权申请联系：
- 官方邮箱：lidecheng@spharx.cn、wangliren@spharx.cn
- 官方网站：https://spharx.cn

---

© 2026 SPHARX Ltd. All Rights Reserved.
