---
layout: default
title: CI/CD流水线
---

# CI/CD流水线展示

<div class="hero-section">
  <h2>自动化CI/CD流水线</h2>
  <p>使用GitHub Actions实现的完整持续集成和持续部署流程</p>
</div>

## 🔄 流水线概览

我们的CI/CD流水线确保代码质量、自动化测试和无缝部署，以下是流水线的各个阶段：

<div class="features-grid">
  <div class="feature-card">
    <h3>📥 代码提交</h3>
    <p>开发者将代码推送到功能分支或主分支，触发CI/CD流水线</p>
  </div>
  
  <div class="feature-card">
    <h3>🧪 自动测试</h3>
    <p>运行单元测试、集成测试和代码质量检查，确保代码质量</p>
  </div>
  
  <div class="feature-card">
    <h3>🏗️ 构建镜像</h3>
    <p>构建Docker镜像，确保环境一致性和可移植性</p>
  </div>
  
  <div class="feature-card">
    <h3>📊 实验运行</h3>
    <p>自动运行ML实验，记录参数和指标到MLflow</p>
  </div>
  
  <div class="feature-card">
    <h3>🚀 部署应用</h3>
    <p>将应用部署到目标环境，支持多环境部署</p>
  </div>
  
  <div class="feature-card">
    <h3>📈 监控反馈</h3>
    <p>监控应用性能和模型表现，提供反馈循环</p>
  </div>
</div>

## 📋 流水线配置

### GitHub Actions工作流

我们的CI/CD流水线使用GitHub Actions实现，以下是主要工作流文件：

#### CI/CD工作流 (.github/workflows/ci-cd.yml)

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [ main, staging ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    
    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.9'
    
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    
    - name: Run tests
      run: |
        pytest tests/ -v
    
    - name: Run linting
      run: |
        flake8 app/ ml/ tests/
        black --check app/ ml/ tests/

  build:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main' || github.ref == 'refs/heads/staging'
    steps:
    - uses: actions/checkout@v3
    
    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v2
    
    - name: Login to Docker Hub
      uses: docker/login-action@v2
      with:
        username: ${{ secrets.DOCKER_USERNAME }}
        password: ${{ secrets.DOCKER_PASSWORD }}
    
    - name: Build and push
      uses: docker/build-push-action@v4
      with:
        context: .
        push: true
        tags: |
          your-username/ml-app:latest
          your-username/ml-app:${{ github.sha }}
    
    - name: Run ML experiments
      run: |
        pip install -r requirements.txt
        python ml/train.py --experiment-name ci-experiment

  deploy:
    needs: build
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:
    - name: Deploy to production
      run: |
        echo "Deploying to production environment"
        # 部署脚本
```

### 流水线触发条件

1. **推送到主分支**：触发完整CI/CD流水线，包括测试、构建和部署
2. **推送到预发布分支**：触发测试和构建，但不部署到生产环境
3. **创建拉取请求**：触发测试和代码质量检查，确保代码质量

## 📊 流水线执行示例

### 成功的流水线执行

```
[CI/CD Pipeline] Run started by user username
[CI/CD Pipeline] Job test passed (2m 15s)
[CI/CD Pipeline] Job build passed (5m 42s)
[CI/CD Pipeline] Job deploy passed (1m 30s)
[CI/CD Pipeline] Run completed successfully
```

### 测试结果示例

```
============================= test session starts =============================
platform linux -- Python 3.9.10, pytest-7.1.2, pluggy-1.0.0
rootdir: /home/runner/work/ml-app-project/ml-app-project
collected 5 items

tests/test_app.py .....                                                [100%]

============================== 5 passed in 12.34s ==============================
```

### 代码质量检查

```
flake8 app/ ml/ tests/
black --check app/ ml/ tests/
All files formatted correctly!
```

## 🔧 环境配置

### 开发环境

```yaml
# docker-compose.dev.yml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/app
    environment:
      - FLASK_ENV=development
      - MLFLOW_TRACKING_URI=http://mlflow:5000
    depends_on:
      - mlflow
      - postgres
  
  mlflow:
    image: python:3.9-slim
    command: >
      bash -c "pip install mlflow psycopg2-binary &&
               mlflow server 
               --backend-store-uri postgresql://mlflow:mlflow@postgres:5432/mlflow
               --default-artifact-root /mlflow/artifacts
               --host 0.0.0.0"
    ports:
      - "5001:5000"
    volumes:
      - mlflow_artifacts:/mlflow/artifacts
    depends_on:
      - postgres
  
  postgres:
    image: postgres:13
    environment:
      - POSTGRES_DB=mlflow
      - POSTGRES_USER=mlflow
      - POSTGRES_PASSWORD=mlflow
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  mlflow_artifacts:
  postgres_data:
```

### 生产环境

```yaml
# docker-compose.prod.yml
version: '3.8'
services:
  app:
    image: your-username/ml-app:latest
    ports:
      - "80:5000"
    environment:
      - FLASK_ENV=production
      - MLFLOW_TRACKING_URI=${MLFLOW_TRACKING_URI}
    restart: unless-stopped
  
  nginx:
    image: nginx:alpine
    ports:
      - "443:443"
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
      - ./ssl:/etc/nginx/ssl
    depends_on:
      - app
    restart: unless-stopped
```

## 📈 流水线优化

### 并行执行

通过优化工作流，我们实现了并行执行测试和构建步骤，减少了总执行时间：

```yaml
jobs:
  test:
    # 测试配置
  
  build:
    needs: test
    # 构建配置
  
  security-scan:
    needs: test
    # 安全扫描配置
  
  deploy:
    needs: [build, security-scan]
    # 部署配置
```

### 缓存优化

使用GitHub Actions缓存减少依赖安装时间：

```yaml
- name: Cache pip dependencies
  uses: actions/cache@v3
  with:
    path: ~/.cache/pip
    key: ${{ runner.os }}-pip-${{ hashFiles('**/requirements.txt') }}
    restore-keys: |
      ${{ runner.os }}-pip-
```

## 🎯 最佳实践

1. **小步提交**：频繁提交小量代码，便于快速发现问题
2. **全面测试**：编写全面的单元测试和集成测试
3. **代码审查**：通过拉取请求进行代码审查
4. **环境隔离**：使用不同环境进行开发、测试和生产
5. **监控反馈**：持续监控应用性能和模型表现
6. **回滚机制**：实现快速回滚机制，处理部署失败情况

## 🔗 相关资源

- [GitHub Actions文档](https://docs.github.com/en/actions)
- [Docker文档](https://docs.docker.com/)
- [MLflow文档](https://mlflow.org/docs/latest/index.html)
- [测试最佳实践](https://docs.pytest.org/en/stable/)