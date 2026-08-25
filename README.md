# 企业财务管控平台 · 经营驾驶舱

面向财务BP（Finance Business Partner）与经营管理者的数据可视化驾驶舱，将营收、成本、利润、现金流、预算、税务、风险等核心财务指标以图表形式直观呈现，支撑经营分析与决策。

> 单文件纯前端应用 · 零依赖 · 双击即开 · 无需后端

---

## 在线演示

👉 **[https://vane1981-2011.github.io/finance-platform/](https://vane1981-2011.github.io/finance-platform/)**

## 本地运行

```bash
# 方式一：直接双击 index.html，浏览器打开即可
# 方式二：任意静态服务器
python3 -m http.server 8000
# 然后访问 http://localhost:8000
```

无需 `npm install`、无需构建、无需后端服务——整个平台就是一个 HTML 文件。

---

## 功能模块

平台围绕财务BP的核心工作场景，划分为 5 大模块：

### 1. 📈 经营驾驶舱
企业整体经营状况的总览，包括：
- 营收 / 成本 / 利润趋势（折线图）
- 月度现金流（柱状图）
- 资金余额趋势（折线图）
- 部门预算执行（柱状图）
- 核心风险指标（环形图）
- 成本结构（环形图）

### 2. 📋 预算管理
- 预算目标 vs 实际营收对比
- 预算差异分析明细

### 3. 💰 资金管理
- 月度现金流分析
- 融资成本对比
- 可选融资方案

### 4. 📑 税务管理
- 税负率趋势
- 税务合规事项清单

### 5. ⚠️ 风险监控
- 核心风险指标监控
- 风险事件日志

---

## 技术栈

| 技术 | 用途 |
|:-----|:-----|
| HTML5 + CSS3 | 页面结构与布局（深色主题，响应式侧边栏） |
| 原生 JavaScript | 交互逻辑、数据渲染、图表初始化 |
| Chart.js 4.x（CDN） | 折线图、柱状图、环形图 |

**设计特点：**

- **单文件架构**：所有 CSS、JS、数据内联在 `index.html` 中，无外部依赖（Chart.js 走 CDN）
- **数据驱动渲染**：图表由 JS 数据数组动态生成，改数据即可更新图表
- **模块化导航**：左侧边栏切换 5 大功能模块，各模块独立渲染

---

## 代码结构

```
finance-platform/
├── index.html      # 全部内容（结构 + 样式 + 逻辑 + 数据）
├── .nojekyll       # 避免 GitHub Pages 用 Jekyll 处理
└── README.md
```

### 核心数据变量（位于 index.html 内）

| 变量 | 含义 |
|:-----|:-----|
| `depts` | 部门列表 |
| `budgetAmt` / `actualAmt` | 各部门预算金额 / 实际金额 |
| `riskIndicators` | 核心风险指标 |
| `budgetVariance` | 预算差异明细 |
| `financingOptions` | 可选融资方案 |
| `taxCompliance` | 税务合规事项 |
| `riskEvents` | 风险事件日志 |
| `currentCharts` | 当前页面的 Chart.js 实例集合 |

---

## 二次开发指南

### 修改数据

所有数据以 JS 数组形式定义在 `index.html` 的 `<script>` 段中。找到对应数组，直接替换数值即可：

```javascript
// 示例：修改部门预算执行数据
var budgetAmt = [120, 80, 60, 95, 70];   // 预算金额
var actualAmt = [108, 92, 55, 88, 74];   // 实际金额
```

### 新增图表

1. 在 HTML 中新增一个 `<canvas id="myChart"></canvas>` 容器
2. 在对应模块的渲染函数中初始化 Chart：

```javascript
var ctx = document.getElementById('myChart').getContext('2d');
currentCharts.push(new Chart(ctx, {
    type: 'bar',           // 可选：line / bar / doughnut / pie
    data: { /* 你的数据 */ },
    options: { /* 你的配置 */ }
}));
```

### 接入真实数据

当前版本使用静态 mock 数据做演示。接入真实数据有两种方式：

1. **纯前端方案**：将后端导出的 JSON 数据粘贴到数据数组中（适合数据量小、更新频率低的场景）
2. **后端方案**：把 `index.html` 作为前端，将数据数组替换为 `fetch('/api/xxx')` 异步拉取，后端提供 REST API（需要新增后端服务）

### 更换主题色

全局配色通过 CSS 变量集中管理，位于 `<style>` 顶部的 `:root` 段：

```css
:root {
  --bg-primary: #0a1628;      /* 主背景 */
  --accent-blue: #3b82f6;     /* 主强调色 */
  --accent-cyan: #06b6d4;     /* 次强调色 */
  /* ... */
}
```

修改这些变量即可全局换肤。

---

## 业务背景

本项目是「财务BP全链路智能体」体系的**可视化前端**部分，配套材料包括：

- 财务管控体系设计方案
- 实际工作使用手册
- 配套案例练习

定位是帮助财务人员从「核算型」向「业务伙伴型（BP）」转型，通过数据可视化把财务数据转化为经营洞察。

---

## License

本项目为个人作品。如需复用或二次开发，请与作者联系授权。
