---
layout: default
title: HTML交互展示
---

# HTML交互展示

<div class="hero-section">
  <h2>交互式HTML元素展示</h2>
  <p>展示项目中的HTML内容和交互元素，提供丰富的用户体验</p>
</div>

## 🎨 HTML组件展示

### 数据可视化组件

以下是我们项目中使用的一些HTML组件示例：

#### 1. 交互式图表

```html
<div class="chart-container">
  <h3>模型性能对比</h3>
  <canvas id="performanceChart" width="400" height="200"></canvas>
  <div class="chart-controls">
    <button id="toggleChartType">切换图表类型</button>
    <select id="modelSelect">
      <option value="all">所有模型</option>
      <option value="rf">随机森林</option>
      <option value="svm">支持向量机</option>
      <option value="nn">神经网络</option>
    </select>
  </div>
</div>
```

#### 2. 参数调节器

```html
<div class="parameter-tuner">
  <h3>模型参数调节</h3>
  <div class="parameter-group">
    <label for="nEstimators">树的数量: <span id="nEstimatorsValue">100</span></label>
    <input type="range" id="nEstimators" min="10" max="200" value="100" class="slider">
  </div>
  <div class="parameter-group">
    <label for="maxDepth">最大深度: <span id="maxDepthValue">6</span></label>
    <input type="range" id="maxDepth" min="1" max="20" value="6" class="slider">
  </div>
  <button id="trainModel" class="btn">训练模型</button>
  <div id="trainingResult" class="result-container"></div>
</div>
```

#### 3. 实验比较表

```html
<div class="experiment-comparison">
  <h3>实验比较</h3>
  <table class="comparison-table">
    <thead>
      <tr>
        <th>实验ID</th>
        <th>模型</th>
        <th>参数</th>
        <th>准确率</th>
        <th>F1分数</th>
        <th>运行时间</th>
        <th>操作</th>
      </tr>
    </thead>
    <tbody id="experimentTableBody">
      <!-- 实验数据将通过JavaScript动态加载 -->
    </tbody>
  </table>
</div>
```

## 🎯 交互式演示

### 模型预测界面

```html
<div class="prediction-interface">
  <h3>鸢尾花分类预测</h3>
  <div class="input-group">
    <label for="sepalLength">花萼长度 (cm):</label>
    <input type="number" id="sepalLength" min="4" max="8" step="0.1" value="5.1">
  </div>
  <div class="input-group">
    <label for="sepalWidth">花萼宽度 (cm):</label>
    <input type="number" id="sepalWidth" min="2" max="5" step="0.1" value="3.5">
  </div>
  <div class="input-group">
    <label for="petalLength">花瓣长度 (cm):</label>
    <input type="number" id="petalLength" min="1" max="7" step="0.1" value="1.4">
  </div>
  <div class="input-group">
    <label for="petalWidth">花瓣宽度 (cm):</label>
    <input type="number" id="petalWidth" min="0.1" max="3" step="0.1" value="0.2">
  </div>
  <button id="predict" class="btn btn-primary">预测</button>
  <div id="predictionResult" class="result-container"></div>
</div>
```

### 实时训练监控

```html
<div class="training-monitor">
  <h3>模型训练监控</h3>
  <div class="monitor-container">
    <div class="metric-card">
      <h4>训练准确率</h4>
      <div class="metric-value" id="trainAccuracy">0.00</div>
      <div class="progress-bar">
        <div class="progress-fill" id="trainAccuracyProgress" style="width: 0%"></div>
      </div>
    </div>
    <div class="metric-card">
      <h4>验证准确率</h4>
      <div class="metric-value" id="valAccuracy">0.00</div>
      <div class="progress-bar">
        <div class="progress-fill" id="valAccuracyProgress" style="width: 0%"></div>
      </div>
    </div>
    <div class="metric-card">
      <h4>训练损失</h4>
      <div class="metric-value" id="trainLoss">0.00</div>
      <div class="progress-bar">
        <div class="progress-fill" id="trainLossProgress" style="width: 0%"></div>
      </div>
    </div>
  </div>
  <div class="training-controls">
    <button id="startTraining" class="btn">开始训练</button>
    <button id="pauseTraining" class="btn btn-secondary">暂停训练</button>
    <button id="resetTraining" class="btn btn-danger">重置训练</button>
  </div>
</div>
```

## 📊 数据表格与过滤

### 实验数据表格

```html
<div class="data-table-container">
  <h3>实验数据</h3>
  <div class="table-controls">
    <input type="text" id="searchInput" placeholder="搜索实验...">
    <select id="statusFilter">
      <option value="">所有状态</option>
      <option value="running">运行中</option>
      <option value="completed">已完成</option>
      <option value="failed">失败</option>
    </select>
    <button id="exportData" class="btn">导出数据</button>
  </div>
  <table class="data-table" id="experimentDataTable">
    <thead>
      <tr>
        <th>实验ID</th>
        <th>名称</th>
        <th>状态</th>
        <th>开始时间</th>
        <th>持续时间</th>
        <th>最佳准确率</th>
        <th>操作</th>
      </tr>
    </thead>
    <tbody>
      <!-- 数据将通过JavaScript动态加载 -->
    </tbody>
  </table>
  <div class="pagination">
    <button id="prevPage" class="btn">上一页</button>
    <span id="pageInfo">第 1 页，共 5 页</span>
    <button id="nextPage" class="btn">下一页</button>
  </div>
</div>
```

## 🎨 CSS样式

以下是我们为这些HTML元素设计的CSS样式：

```css
/* 图表容器样式 */
.chart-container {
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  margin-bottom: 20px;
}

.chart-controls {
  margin-top: 15px;
  display: flex;
  gap: 10px;
  align-items: center;
}

/* 参数调节器样式 */
.parameter-tuner {
  background-color: #f8f9fa;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 20px;
}

.parameter-group {
  margin-bottom: 15px;
}

.slider {
  width: 100%;
  margin-top: 5px;
}

/* 预测界面样式 */
.prediction-interface {
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  margin-bottom: 20px;
}

.input-group {
  margin-bottom: 15px;
}

.input-group label {
  display: block;
  margin-bottom: 5px;
  font-weight: 500;
}

.input-group input {
  width: 100%;
  padding: 8px 12px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

/* 训练监控样式 */
.training-monitor {
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  margin-bottom: 20px;
}

.monitor-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 15px;
  margin-bottom: 20px;
}

.metric-card {
  background-color: #f8f9fa;
  border-radius: 8px;
  padding: 15px;
  text-align: center;
}

.metric-value {
  font-size: 24px;
  font-weight: bold;
  margin: 10px 0;
}

.progress-bar {
  height: 10px;
  background-color: #e9ecef;
  border-radius: 5px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  background-color: #007bff;
  transition: width 0.3s ease;
}

/* 数据表格样式 */
.data-table-container {
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  margin-bottom: 20px;
}

.table-controls {
  display: flex;
  gap: 10px;
  margin-bottom: 15px;
  flex-wrap: wrap;
}

.table-controls input,
.table-controls select {
  padding: 8px 12px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.data-table {
  width: 100%;
  border-collapse: collapse;
  margin-bottom: 15px;
}

.data-table th,
.data-table td {
  padding: 12px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

.data-table th {
  background-color: #f8f9fa;
  font-weight: 600;
}

.data-table tr:hover {
  background-color: #f8f9fa;
}

.pagination {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* 按钮样式 */
.btn {
  display: inline-block;
  padding: 8px 16px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  text-decoration: none;
  transition: background-color 0.2s;
}

.btn:hover {
  background-color: #0069d9;
}

.btn-secondary {
  background-color: #6c757d;
}

.btn-secondary:hover {
  background-color: #5a6268;
}

.btn-danger {
  background-color: #dc3545;
}

.btn-danger:hover {
  background-color: #c82333;
}

/* 结果容器样式 */
.result-container {
  margin-top: 15px;
  padding: 15px;
  border-radius: 4px;
  background-color: #f8f9fa;
  border-left: 4px solid #007bff;
}
```

## 🔄 JavaScript交互

以下是一些实现这些HTML元素交互的JavaScript代码：

```javascript
// 图表类型切换
document.getElementById('toggleChartType').addEventListener('click', function() {
  // 切换图表类型的逻辑
  const chart = document.getElementById('performanceChart');
  // 更新图表
});

// 参数滑块更新
document.getElementById('nEstimators').addEventListener('input', function() {
  document.getElementById('nEstimatorsValue').textContent = this.value;
});

document.getElementById('maxDepth').addEventListener('input', function() {
  document.getElementById('maxDepthValue').textContent = this.value;
});

// 模型训练
document.getElementById('trainModel').addEventListener('click', function() {
  const nEstimators = document.getElementById('nEstimators').value;
  const maxDepth = document.getElementById('maxDepth').value;
  
  // 显示加载状态
  const resultContainer = document.getElementById('trainingResult');
  resultContainer.innerHTML = '<div class="loading">训练中...</div>';
  
  // 发送训练请求
  fetch('/api/train', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      n_estimators: parseInt(nEstimators),
      max_depth: parseInt(maxDepth)
    })
  })
  .then(response => response.json())
  .then(data => {
    // 显示训练结果
    resultContainer.innerHTML = `
      <div class="result">
        <h4>训练结果</h4>
        <p>准确率: ${data.accuracy.toFixed(4)}</p>
        <p>F1分数: ${data.f1_score.toFixed(4)}</p>
        <p>训练时间: ${data.training_time}秒</p>
      </div>
    `;
  })
  .catch(error => {
    resultContainer.innerHTML = `<div class="error">训练失败: ${error.message}</div>`;
  });
});

// 预测功能
document.getElementById('predict').addEventListener('click', function() {
  const sepalLength = document.getElementById('sepalLength').value;
  const sepalWidth = document.getElementById('sepalWidth').value;
  const petalLength = document.getElementById('petalLength').value;
  const petalWidth = document.getElementById('petalWidth').value;
  
  // 显示加载状态
  const resultContainer = document.getElementById('predictionResult');
  resultContainer.innerHTML = '<div class="loading">预测中...</div>';
  
  // 发送预测请求
  fetch('/api/predict', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      sepal_length: parseFloat(sepalLength),
      sepal_width: parseFloat(sepalWidth),
      petal_length: parseFloat(petalLength),
      petal_width: parseFloat(petalWidth)
    })
  })
  .then(response => response.json())
  .then(data => {
    // 显示预测结果
    resultContainer.innerHTML = `
      <div class="result">
        <h4>预测结果</h4>
        <p>预测类别: ${data.prediction}</p>
        <p>置信度: ${(data.confidence * 100).toFixed(2)}%</p>
      </div>
    `;
  })
  .catch(error => {
    resultContainer.innerHTML = `<div class="error">预测失败: ${error.message}</div>`;
  });
});

// 训练监控
let trainingInterval;

document.getElementById('startTraining').addEventListener('click', function() {
  // 开始训练监控
  trainingInterval = setInterval(updateTrainingMetrics, 1000);
});

document.getElementById('pauseTraining').addEventListener('click', function() {
  // 暂停训练监控
  clearInterval(trainingInterval);
});

document.getElementById('resetTraining').addEventListener('click', function() {
  // 重置训练监控
  clearInterval(trainingInterval);
  document.getElementById('trainAccuracy').textContent = '0.00';
  document.getElementById('valAccuracy').textContent = '0.00';
  document.getElementById('trainLoss').textContent = '0.00';
  document.getElementById('trainAccuracyProgress').style.width = '0%';
  document.getElementById('valAccuracyProgress').style.width = '0%';
  document.getElementById('trainLossProgress').style.width = '0%';
});

function updateTrainingMetrics() {
  // 模拟训练指标更新
  const trainAccuracy = Math.min(0.99, parseFloat(document.getElementById('trainAccuracy').textContent) + Math.random() * 0.05);
  const valAccuracy = Math.min(0.95, parseFloat(document.getElementById('valAccuracy').textContent) + Math.random() * 0.04);
  const trainLoss = Math.max(0.01, parseFloat(document.getElementById('trainLoss').textContent) - Math.random() * 0.02);
  
  document.getElementById('trainAccuracy').textContent = trainAccuracy.toFixed(2);
  document.getElementById('valAccuracy').textContent = valAccuracy.toFixed(2);
  document.getElementById('trainLoss').textContent = trainLoss.toFixed(2);
  
  document.getElementById('trainAccuracyProgress').style.width = `${trainAccuracy * 100}%`;
  document.getElementById('valAccuracyProgress').style.width = `${valAccuracy * 100}%`;
  document.getElementById('trainLossProgress').style.width = `${(1 - trainLoss) * 100}%`;
}

// 数据表格搜索和过滤
document.getElementById('searchInput').addEventListener('input', filterTable);
document.getElementById('statusFilter').addEventListener('change', filterTable);

function filterTable() {
  const searchInput = document.getElementById('searchInput').value.toLowerCase();
  const statusFilter = document.getElementById('statusFilter').value;
  const table = document.getElementById('experimentDataTable');
  const rows = table.getElementsByTagName('tr');
  
  for (let i = 1; i < rows.length; i++) {
    const experimentId = rows[i].cells[0].textContent.toLowerCase();
    const name = rows[i].cells[1].textContent.toLowerCase();
    const status = rows[i].cells[2].textContent.toLowerCase();
    
    const matchesSearch = experimentId.includes(searchInput) || name.includes(searchInput);
    const matchesStatus = !statusFilter || status === statusFilter.toLowerCase();
    
    rows[i].style.display = matchesSearch && matchesStatus ? '' : 'none';
  }
}

// 数据导出
document.getElementById('exportData').addEventListener('click', function() {
  // 导出表格数据为CSV
  const table = document.getElementById('experimentDataTable');
  let csv = [];
  
  for (let i = 0; i < table.rows.length; i++) {
    const row = [];
    for (let j = 0; j < table.rows[i].cells.length; j++) {
      row.push(table.rows[i].cells[j].textContent);
    }
    csv.push(row.join(','));
  }
  
  const csvContent = csv.join('\n');
  const blob = new Blob([csvContent], { type: 'text/csv' });
  const url = URL.createObjectURL(blob);
  
  const a = document.createElement('a');
  a.href = url;
  a.download = 'experiments.csv';
  a.click();
  
  URL.revokeObjectURL(url);
});
```

## 🌐 集成到Jekyll

要将这些HTML元素集成到Jekyll网站中，您可以：

1. 创建包含HTML内容的Markdown文件
2. 使用Jekyll的`include`功能重用组件
3. 将CSS和JavaScript代码添加到`assets/css`和`assets/js`目录
4. 在`_config.yml`中配置包含目录

例如，直接在Markdown文件中嵌入HTML代码：

```html
<div class="chart-container">
  <h3>模型性能对比</h3>
  <canvas id="performanceChart" width="400" height="200"></canvas>
  <div class="chart-controls">
    <!-- 控制按钮可以在这里添加 -->
  </div>
</div>
```

## 🔗 相关资源

- [HTML5规范](https://html.spec.whatwg.org/)
- [MDN Web文档](https://developer.mozilla.org/zh-CN/docs/Web/HTML)
- [Bootstrap文档](https://getbootstrap.com/docs/)
- [Chart.js文档](https://www.chartjs.org/docs/latest/)