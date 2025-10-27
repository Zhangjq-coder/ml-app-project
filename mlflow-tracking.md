---
layout: default
title: MLflow实验跟踪
---

# MLflow实验跟踪展示

<div class="hero-section">
  <h2>MLflow实验跟踪系统</h2>
  <p>使用MLflow进行全面的机器学习实验管理、参数跟踪和模型版本控制</p>
</div>

## 📊 MLflow概述

MLflow是一个开源平台，用于管理端到端的机器学习生命周期。它提供了以下核心功能：

<div class="features-grid">
  <div class="feature-card">
    <h3>🔍 实验跟踪</h3>
    <p>记录和查询实验数据，包括参数、指标和产物</p>
  </div>
  
  <div class="feature-card">
    <h3>📦 打包代码</h3>
    <p>以可重现的方式打包ML代码，便于共享和部署</p>
  </div>
  
  <div class="feature-card">
    <h3>🏷️ 模型管理</h3>
    <p>集中管理模型，支持版本控制、阶段转换和注释</p>
  </div>
  
  <div class="feature-card">
    <h3>👥 模型服务</h3>
    <p>将ML模型部署为REST API，便于集成和应用</p>
  </div>
</div>

## 🧪 实验跟踪示例

### 基本实验记录

```python
import mlflow
import mlflow.sklearn
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score
from sklearn.model_selection import train_test_split
import pandas as pd

# 加载数据
data = pd.read_csv('data/iris.csv')
X = data.drop('target', axis=1)
y = data['target']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# 设置实验
mlflow.set_experiment("Iris Classification")

# 开始实验运行
with mlflow.start_run():
    # 设置参数
    n_estimators = 100
    max_depth = 6
    random_state = 42
    
    # 记录参数
    mlflow.log_param("n_estimators", n_estimators)
    mlflow.log_param("max_depth", max_depth)
    mlflow.log_param("random_state", random_state)
    
    # 训练模型
    model = RandomForestClassifier(
        n_estimators=n_estimators,
        max_depth=max_depth,
        random_state=random_state
    )
    model.fit(X_train, y_train)
    
    # 预测和评估
    y_pred = model.predict(X_test)
    accuracy = accuracy_score(y_test, y_pred)
    
    # 记录指标
    mlflow.log_metric("accuracy", accuracy)
    
    # 记录模型
    mlflow.sklearn.log_model(model, "model")
    
    # 记录其他产物
    mlflow.log_artifact("data/iris.csv", "dataset")
    
    print(f"Model accuracy: {accuracy}")
```

### 高级实验跟踪

```python
import mlflow
import mlflow.sklearn
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.metrics import confusion_matrix, classification_report
import numpy as np

# 设置实验
mlflow.set_experiment("Advanced Iris Classification")

# 开始实验运行
with mlflow.start_run(run_name="Random Forest with Confusion Matrix"):
    # 设置参数
    params = {
        "n_estimators": 100,
        "max_depth": 6,
        "min_samples_split": 2,
        "min_samples_leaf": 1,
        "random_state": 42
    }
    
    # 记录参数
    mlflow.log_params(params)
    
    # 训练模型
    model = RandomForestClassifier(**params)
    model.fit(X_train, y_train)
    
    # 预测和评估
    y_pred = model.predict(X_test)
    accuracy = accuracy_score(y_test, y_pred)
    
    # 记录指标
    mlflow.log_metric("accuracy", accuracy)
    
    # 生成并记录混淆矩阵
    cm = confusion_matrix(y_test, y_pred)
    plt.figure(figsize=(8, 6))
    sns.heatmap(cm, annot=True, fmt='d', cmap='Blues')
    plt.xlabel('Predicted')
    plt.ylabel('Actual')
    plt.title('Confusion Matrix')
    
    # 保存图表
    confusion_matrix_path = "confusion_matrix.png"
    plt.savefig(confusion_matrix_path)
    mlflow.log_artifact(confusion_matrix_path, "plots")
    
    # 记录分类报告
    report = classification_report(y_test, y_pred, output_dict=True)
    for class_name, metrics in report.items():
        if isinstance(metrics, dict):
            for metric_name, value in metrics.items():
                mlflow.log_metric(f"{class_name}_{metric_name}", value)
    
    # 记录模型
    mlflow.sklearn.log_model(model, "model")
    
    # 记录特征重要性
    feature_importance = model.feature_importances_
    for i, importance in enumerate(feature_importance):
        mlflow.log_metric(f"feature_{i}_importance", importance)
    
    print(f"Model accuracy: {accuracy}")
```

## 🏷️ 模型注册与管理

### 模型注册示例

```python
import mlflow
import mlflow.sklearn

# 训练模型
model = RandomForestClassifier(n_estimators=100, max_depth=6, random_state=42)
model.fit(X_train, y_train)

# 记录模型到注册表
with mlflow.start_run() as run:
    # 记录模型
    mlflow.sklearn.log_model(
        model, 
        "model",
        registered_model_name="IrisClassifier"
    )
    
    # 获取模型版本
    model_version = run.info.run_id
    print(f"Model version: {model_version}")
```

### 模型阶段转换

```python
import mlflow
from mlflow.tracking import MlflowClient

client = MlflowClient()

# 获取最新版本的模型
model_name = "IrisClassifier"
model_version_infos = client.search_model_versions(f"name='{model_name}'")
latest_version = max([int(info.version) for info in model_version_infos])

# 将模型从Staging转换为Production
client.transition_model_version_stage(
    name=model_name,
    version=latest_version,
    stage="Production",
    archive_existing_versions=True
)

print(f"Model {model_name} version {latest_version} is now in Production stage")
```

### 模型加载与预测

```python
import mlflow.pyfunc

# 加载生产阶段的模型
model_name = "IrisClassifier"
stage = "Production"

model_uri = f"models:/{model_name}/{stage}"
model = mlflow.pyfunc.load_model(model_uri)

# 进行预测
import pandas as pd
sample_data = pd.DataFrame({
    'sepal_length': [5.1, 6.2],
    'sepal_width': [3.5, 3.4],
    'petal_length': [1.4, 5.4],
    'petal_width': [0.2, 2.3]
})

predictions = model.predict(sample_data)
print(f"Predictions: {predictions}")
```

## 🖥️ MLflow UI展示

MLflow提供了一个直观的Web界面，用于查看和比较实验：

### 实验列表视图

```
实验名称                    | 运行次数 | 最后更新时间
Iris Classification        | 15       | 2023-05-15 14:30
Advanced Iris Classification| 8        | 2023-05-15 12:45
Hyperparameter Tuning      | 25       | 2023-05-14 18:20
```

### 实验运行详情

```
运行ID: 7d5e9f3a2b1c4d5e
开始时间: 2023-05-15 14:25:30
状态: 已完成
持续时间: 2分15秒

参数:
- n_estimators: 100
- max_depth: 6
- random_state: 42

指标:
- accuracy: 0.9667
- setosa_precision: 1.0
- setosa_recall: 1.0
- setosa_f1-score: 1.0

产物:
- model: sklearn模型
- confusion_matrix.png: 混淆矩阵图表
- dataset: iris.csv
```

### 模型比较视图

```
模型名称                   | 版本 | 阶段      | 准确率
IrisClassifier            | 1    | Staging   | 0.9500
IrisClassifier            | 2    | Production| 0.9667
IrisClassifier            | 3    | Staging   | 0.9833
```

## 🔄 实验工作流

### 自动化实验运行

```python
import mlflow
import itertools
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score

# 设置实验
mlflow.set_experiment("Hyperparameter Tuning")

# 定义超参数网格
param_grid = {
    'n_estimators': [50, 100, 200],
    'max_depth': [3, 6, 9],
    'min_samples_split': [2, 5, 10]
}

# 生成所有参数组合
param_combinations = list(itertools.product(
    param_grid['n_estimators'],
    param_grid['max_depth'],
    param_grid['min_samples_split']
))

# 运行实验
for params in param_combinations:
    n_estimators, max_depth, min_samples_split = params
    
    with mlflow.start_run():
        # 记录参数
        mlflow.log_params({
            'n_estimators': n_estimators,
            'max_depth': max_depth,
            'min_samples_split': min_samples_split
        })
        
        # 训练模型
        model = RandomForestClassifier(
            n_estimators=n_estimators,
            max_depth=max_depth,
            min_samples_split=min_samples_split,
            random_state=42
        )
        model.fit(X_train, y_train)
        
        # 评估模型
        y_pred = model.predict(X_test)
        accuracy = accuracy_score(y_test, y_pred)
        
        # 记录指标
        mlflow.log_metric("accuracy", accuracy)
        
        # 记录模型
        mlflow.sklearn.log_model(model, "model")
        
        print(f"Params: {params}, Accuracy: {accuracy:.4f}")
```

## 🐳 Docker中的MLflow

### MLflow服务器Docker配置

```dockerfile
# Dockerfile.mlflow
FROM python:3.9-slim

WORKDIR /app

# 安装MLflow和数据库驱动
RUN pip install mlflow psycopg2-binary

# 创建非root用户
RUN useradd --create-home --shell /bin/bash mlflow
USER mlflow

# 暴露端口
EXPOSE 5000

# 启动MLflow服务器
CMD ["mlflow", "server", 
      "--backend-store-uri", "postgresql://mlflow:mlflow@postgres:5432/mlflow",
      "--default-artifact-root", "/mlflow/artifacts",
      "--host", "0.0.0.0"]
```

### Docker Compose配置

```yaml
# docker-compose.mlflow.yml
version: '3.8'
services:
  mlflow:
    build:
      context: .
      dockerfile: Dockerfile.mlflow
    ports:
      - "5000:5000"
    volumes:
      - mlflow_artifacts:/mlflow/artifacts
    environment:
      - MLFLOW_BACKEND_STORE_URI=postgresql://mlflow:mlflow@postgres:5432/mlflow
      - MLFLOW_DEFAULT_ARTIFACT_ROOT=/mlflow/artifacts
    depends_on:
      - postgres
    restart: unless-stopped
  
  postgres:
    image: postgres:13
    environment:
      - POSTGRES_DB=mlflow
      - POSTGRES_USER=mlflow
      - POSTGRES_PASSWORD=mlflow
    volumes:
      - postgres_data:/var/lib/postgresql/data
    restart: unless-stopped

volumes:
  mlflow_artifacts:
  postgres_data:
```

## 📈 最佳实践

1. **结构化实验**：为不同类型实验创建不同的实验名称
2. **参数记录**：记录所有影响模型性能的参数
3. **指标跟踪**：记录关键性能指标和业务指标
4. **模型版本控制**：使用模型注册表管理模型版本
5. **产物管理**：记录重要的图表、数据集和配置文件
6. **环境一致性**：记录运行环境和依赖信息
7. **可重现性**：确保实验可以完全重现

## 🔗 相关资源

- [MLflow官方文档](https://mlflow.org/docs/latest/index.html)
- [MLflow跟踪API参考](https://mlflow.org/docs/latest/python_api/mlflow.html)
- [MLflow模型注册](https://mlflow.org/docs/latest/model-registry.html)
- [MLflow模型服务](https://mlflow.org/docs/latest/models.html)