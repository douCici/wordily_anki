# Wordily 微信小程序技术架构

本文档描述 Wordily 项目的整体技术架构，并给出主要 API 接口定义。

## 架构示意图

```svg
<svg width="440" height="360" xmlns="http://www.w3.org/2000/svg">
  <style>
    .box { fill: #f5f5f5; stroke: #555; }
    .title { font: bold 14px sans-serif; }
    .text { font: 12px sans-serif; }
    .arrow { stroke: #555; marker-end: url(#arr); fill: none; }
  </style>
  <defs>
    <marker id="arr" viewBox="0 0 10 10" refX="10" refY="5" markerWidth="6" markerHeight="6" orient="auto">
      <path d="M 0 0 L 10 5 L 0 10 z" fill="#555" />
    </marker>
  </defs>

  <!-- 微信小程序 -->
  <rect x="20" y="20" width="180" height="60" class="box" />
  <text x="110" y="40" text-anchor="middle" class="title">微信小程序</text>
  <text x="110" y="60" text-anchor="middle" class="text">用户交互与展示</text>

  <!-- API 服务 -->
  <rect x="240" y="20" width="180" height="120" class="box" />
  <text x="330" y="40" text-anchor="middle" class="title">后端 API 服务</text>
  <text x="330" y="60" text-anchor="middle" class="text">FastAPI + Anki 引擎</text>
  <text x="330" y="80" text-anchor="middle" class="text">GPT 调用模块</text>
  <text x="330" y="100" text-anchor="middle" class="text">认证与日志</text>

  <!-- 数据库 -->
  <rect x="240" y="170" width="180" height="60" class="box" />
  <text x="330" y="190" text-anchor="middle" class="title">云端数据库</text>
  <text x="330" y="210" text-anchor="middle" class="text">存储卡片与进度</text>

  <!-- 箭头 -->
  <path class="arrow" d="M200 50 L240 50" />
  <path class="arrow" d="M330 140 L330 170" />
</svg>
```

## API 接口定义（示例）

| 接口 | 方法 | 描述 | 请求参数 | 返回值 |
| ---- | ---- | ---- | -------- | ------ |
| `/api/cards` | `POST` | 创建新卡片 | `text`: 待记忆内容 | `card_id` |
| `/api/reviews` | `GET` | 获取待复习卡片列表 | `user_id` | 卡片数组 |
| `/api/review/{id}` | `POST` | 提交复习结果 | `rating`: Again/Hard/... | 更新后的间隔等 |
| `/api/stats` | `GET` | 获取打卡统计 | `user_id` | 完成次数等 |
| `/api/gpt` | `POST` | 调用 GPT 生成释义/例句 | `text` | AI 生成内容 |

以上接口仅供参考，可根据实际需求扩展认证、分页等功能。
