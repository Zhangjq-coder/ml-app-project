---
layout: default
title: Home
---

# MLOps Project Demo

<div class="hero-section">
  <h2>企业级机器学习运维完整解决方案</h2>
  <p>一个全面的MLOps项目，展示数据版本控制、实验跟踪和CI/CD流水线的最佳实践</p>
</div>

## 🌟 核心特性

<div class="features-grid">
  <div class="feature-card">
    <h3>🔄 数据版本控制</h3>
    <p>使用DVC进行数据变更跟踪和管理，确保数据可追溯性和可重现性</p>
  </div>
  
  <div class="feature-card">
    <h3>📊 实验跟踪</h3>
    <p>使用MLflow跟踪机器学习实验，记录参数、指标和模型版本</p>
  </div>
  
  <div class="feature-card">
    <h3>🚀 CI/CD流水线</h3>
    <p>使用GitHub Actions实现自动化测试和部署，提高开发效率</p>
  </div>
  
  <div class="feature-card">
    <h3>🐳 容器化</h3>
    <p>Docker支持确保环境可重现性，简化部署流程</p>
  </div>
  
  <div class="feature-card">
    <h3>📚 完整文档</h3>
    <p>提供全面的文档和指南，便于理解和复现</p>
  </div>
  
  <div class="feature-card">
    <h3>🔧 模型服务</h3>
    <p>模型部署和服务化，支持RESTful API调用</p>
  </div>
</div>

## 🎯 演示亮点

### 数据版本控制演示

```bash
# 初始化DVC
dvc init

# 跟踪数据文件
dvc add data/iris_v1.csv
dvc add data/iris_v2.csv

# 检查数据变更
dvc diff
```

### 实验跟踪演示

```bash
# 启动MLflow UI
mlflow ui

# 运行实验
python ml/train.py --experiment-name iris_classification

# 比较实验结果
mlflow ui
```

### 容器化演示

```bash
# 构建Docker镜像
docker build -t ml-app .

# 使用Docker Compose运行
docker-compose up
```

## 🏗️ 项目架构

```
ml-app-project/
├── app/           # Flask应用程序
├── ml/            # 机器学习代码
├── data/          # 数据文件
├── tests/         # 测试文件
├── .github/       # GitHub工作流
├── Dockerfile     # Docker配置
└── docker-compose.yml  # Docker Compose配置
```

## 🚀 快速开始

1. 克隆仓库
2. 安装依赖：`pip install -r requirements.txt`
3. 初始化DVC：`dvc init`
4. 拉取数据：`dvc pull`
5. 运行应用程序：`python app/main.py`

## 📖 文档导航

<div class="doc-nav">
  <a href="/api">API文档</a>
  <a href="/demo-guide">演示指南</a>
  <a href="/mlops-components">MLOps组件</a>
  <a href="/ci-cd">CI/CD流水线</a>
  <a href="/mlflow-tracking">MLflow实验跟踪</a>
  <a href="/html-showcase">HTML交互展示</a>
</div>

## 🎓 学习价值

本项目展示了完整的MLOps生命周期，包括：

- 数据准备和版本控制
- 模型开发和实验跟踪
- 模型评估和选择
- 模型部署和服务
- 监控和维护

通过这个项目，您将学习如何构建可扩展、可维护的机器学习系统，以及如何使用现代MLOps工具提高开发效率。