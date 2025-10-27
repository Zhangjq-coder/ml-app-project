# ML App Project: 端到端机器学习应用演示

[![CI/CD](https://github.com/Zhangjq-coder/ml-app-project/actions/workflows/ci-cd.yml/badge.svg)](https://github.com/Zhangjq-coder/ml-app-project/actions/workflows/ci-cd.yml)
[![GitHub Pages](https://github.com/Zhangjq-coder/ml-app-project/actions/workflows/pages.yml/badge.svg)](https://zhangjq-coder.github.io/ml-app-project/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

这个项目展示了一个完整的机器学习应用，集成了现代化的DevOps和MLOps实践，包括数据版本控制、实验跟踪、持续集成/持续部署(CI/CD)和容器化部署。

## 🌟 项目亮点

- **端到端ML流程**: 从数据准备到模型部署的完整机器学习生命周期
- **数据版本控制**: 使用DVC进行数据版本管理和跟踪
- **实验跟踪**: 使用MLflow记录和比较实验结果
- **CI/CD流水线**: 自动化测试、构建和部署流程
- **容器化部署**: 使用Docker进行应用容器化
- **文档化**: 完整的项目文档和API文档

## 🏗️ 项目架构

```
.
├── app/                 # 应用程序代码
│   ├── api/            # API接口
│   ├── core/           # 核心业务逻辑
│   └── main.py         # 应用入口
├── ml/                 # 机器学习组件
│   ├── configs/        # 模型配置
│   ├── data/           # 数据处理
│   ├── models/         # 模型定义
│   └── registry/       # 模型注册
├── data/               # 数据目录 (由DVC跟踪)
├── tests/              # 测试套件
├── docs/               # 项目文档
├── .github/workflows/  # CI/CD流水线
├── Dockerfile          # Docker配置
├── requirements.txt    # Python依赖
├── Gemfile             # Jekyll依赖 (用于文档)
└── README.md          # 项目说明
```

## 🚀 快速开始

### 环境准备

1. 克隆仓库
   ```bash
   git clone https://github.com/Zhangjq-coder/ml-app-project.git
   cd ml-app-project
   ```

2. 创建虚拟环境
   ```bash
   python -m venv venv
   
   # Windows
   venv\Scripts\activate
   
   # Unix/Linux
   source venv/bin/activate
   ```

3. 安装依赖
   ```bash
   pip install -r requirements.txt
   ```

### 数据准备

1. 初始化DVC
   ```bash
   dvc init
   ```

2. 配置远程存储 (可选)
   ```bash
   dvc remote add -d myremote /path/to/remote/storage
   ```

3. 获取数据
   ```bash
   dvc pull
   ```

### 运行应用

1. 启动MLflow跟踪服务器
   ```bash
   mlflow ui
   ```

2. 运行应用
   ```bash
   python app/main.py
   ```

3. 构建Docker镜像 (可选)
   ```bash
   docker build -t ml-app .
   docker run -p 8000:8000 ml-app
   ```

## 🔄 开发工作流

### Git分支策略

- `main`: 生产环境代码
- `staging`: 预生产环境代码
- `dev`: 开发环境代码
- `feature/*`: 功能开发分支

### CI/CD流水线

- **拉取请求到受保护分支时**:
  - 运行测试套件
  - 运行代码检查/格式化/静态分析
  - 构建Docker镜像

- **合并到staging分支时**:
  - 创建staging环境
  - 构建staging Docker镜像

- **合并到main分支时**:
  - 创建生产环境
  - 构建生产Docker镜像

## 📊 MLOps实践

### 数据版本控制 (DVC)

数据使用DVC进行版本控制。原始数据存储在Azure存储中，Git中只跟踪.dvc指针文件。

### 实验跟踪 (MLflow)

ML实验使用MLflow进行跟踪。每次运行记录:
- 代码版本 (Git提交SHA)
- 数据集版本 (DVC数据集版本)
- 超参数
- 评估指标
- 产物 (模型、图表)

### 模型注册

模型使用MLflow Model Registry进行管理:
- 模型版本控制
- 阶段转换 (Staging → Production)
- 模型性能监控

## 📖 文档

- [项目文档](https://zhangjq-coder.github.io/ml-app-project/) - 详细的项目文档和API参考
- [DVC文档](https://dvc.org/doc) - 数据版本控制指南
- [MLflow文档](https://mlflow.org/docs/latest/index.html) - 实验跟踪指南

## 🤝 贡献

欢迎贡献代码！请遵循以下步骤:

1. Fork项目
2. 创建功能分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 创建拉取请求

## 📄 许可证

本项目采用MIT许可证 - 查看 [LICENSE](LICENSE) 文件了解详情。

## 🙏 致谢

- [DVC](https://dvc.org/) - 数据版本控制
- [MLflow](https://mlflow.org/) - 机器学习生命周期管理
- [FastAPI](https://fastapi.tiangolo.com/) - 现代Web框架
- [Docker](https://www.docker.com/) - 容器化平台