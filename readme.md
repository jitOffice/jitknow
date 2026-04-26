<div align="center">

<img src="https://know.jitword.com/public/uploads/know-logo_19d18ea166a.png" width="120" alt="JitKnow Logo" style="border-radius:16px"/>

# JitKnow API 开放平台

**企业级 AI 知识库 · 开发者接入文档**

[![API Version](https://img.shields.io/badge/API-v1-165DFF?style=flat-square&logo=swagger)](https://know.jitword.com)
[![SSE Stream](https://img.shields.io/badge/Stream-SSE-10B981?style=flat-square&logo=lightning)](https://know.jitword.com)
[![Auth](https://img.shields.io/badge/Auth-Bearer_Token-8B5CF6?style=flat-square&logo=shield)](https://know.jitword.com)
[![License](https://img.shields.io/badge/License-Commercial-F59E0B?style=flat-square)](https://know.jitword.com)
[![Contact](https://img.shields.io/badge/WeChat-cxzk__168-07C160?style=flat-square&logo=wechat)](https://know.jitword.com)

> 🚀 **5 分钟接入**，让你的网站、App、内部系统拥有专属 AI 知识库问答能力。  
> 嵌入式 Widget · RESTful Chat API · SSE 流式输出 · Citations 知识引用溯源

[立即体验](https://know.jitword.com/know/login) · [查看在线文档](https://jitword.com) · [技术支持](https://know.jitword.com)

</div>

---

## 目录

- [✨ 产品简介](#-产品简介)
- [🗺️ 能力全景](#️-能力全景)
- [⚡ 快速开始（5步）](#-快速开始5步)
- [📦 嵌入式 Widget 接入](#-嵌入式-widget-接入)
  - [悬浮气泡 Widget](#悬浮气泡-widget)
  - [iframe 嵌入](#iframe-嵌入)
  - [JitMindConfig 参数说明](#jitmindconfig-参数说明)
- [📡 API 参考文档](#-api-参考文档)
  - [鉴权方式](#鉴权方式)
  - [GET /info · 获取助手信息](#get-info--获取助手信息)
  - [POST /chat · 发起流式对话](#post-chat--发起流式对话-sse)
  - [SSE 事件说明](#sse-事件说明)
- [💻 多语言代码示例](#-多语言代码示例)
  - [cURL](#curl)
  - [JavaScript](#javascript)
  - [Python](#python)
- [🔐 安全与限流](#-安全与限流)
- [🚨 错误码参考](#-错误码参考)
- [❓ 常见问题 FAQ](#-常见问题-faq)
- [📞 联系我们](#-联系我们)

---

## ✨ 产品简介

JitKnow 是企业级 **AI 智能知识库平台**，支持将 PDF、Word、Excel、网页等 20+ 格式文档构建为专属 AI 知识库，通过 RAG（检索增强生成）技术实现精准问答。

**JitKnow 开放平台** 将这套 AI 能力以 API 形式开放给第三方开发者，典型应用场景包括：

| 场景 | 描述 |
|------|------|
| 🌐 **官网智能客服** | 将产品手册 AI 助手嵌入官网，替代人工客服 |
| 💼 **企业内部工具** | 将 HR / 法务 / 技术文档助手集成到 OA、钉钉、飞书 |
| 🤖 **App 内 AI 问答** | 通过 API 在移动端实现 AI 知识库问答 |
| ⚙️ **SaaS 产品增强** | 为自家 SaaS 产品嵌入 AI 问答模块，提升用户体验 |

---

## 🗺️ 能力全景

```
┌─────────────────────────────────────────────────────────────┐
│                    JitKnow 开放平台                          │
├─────────────────┬─────────────────┬─────────────────────────┤
│  📦 嵌入式 Widget │  📡 Chat API    │  🔐 安全与管控           │
├─────────────────┼─────────────────┼─────────────────────────┤
│ 悬浮气泡 Widget  │ GET  /info      │ API Key 权限隔离         │
│ iframe 嵌入     │ POST /chat (SSE)│ IP 白名单访问控制        │
│ 深色/浅色主题   │ 多轮对话上下文  │ RPM 速率限流             │
│ 自定义颜色位置  │ Citations 溯源  │ 日调用配额               │
│ 1行代码接入     │ 流式实时输出    │ Key 过期时间管理         │
└─────────────────┴─────────────────┴─────────────────────────┘
```

**核心优势对比：**

| 能力 | JitKnow | Dify | Coze |
|------|:-------:|:----:|:----:|
| API Key 管理（多 Key + 配额） | ✅ | ✅ | ✅ |
| SSE 流式输出 | ✅ | ✅ | ✅ |
| 多轮对话 `conversationId` | ✅ | ✅ | ✅ |
| **Citations 知识引用溯源** | ✅ **核心差异** | ✅ | ⚠️ 有限 |
| IP 白名单 | ✅ | ⚠️ 企业版 | ❌ |
| 嵌入式 Widget（embed.js） | ✅ | ✅ | ✅ |
| 私有化部署后自托管 API | ✅ | ✅ | ❌ |
| 企业知识库原生绑定 | ✅ **核心差异** | ⚠️ 通用 | ⚠️ 通用 |

---

## ⚡ 快速开始（5步）

### Step 1 · 注册并创建 AI 助手

前往 [JitKnow 平台](https://know.jitword.com/know/login) 注册账户，创建一个 AI 助手，上传你的产品文档、FAQ、知识文章，构建专属知识库。

### Step 2 · 获取 API Key

进入 **助手详情页 → API 接入 Tab → 创建 API Key**，记录你的：

- `assistantId`：助手唯一 ID
- API Key：格式为 `jk-xxxxxxxxxxxxxxxx`

> ⚠️ **安全提醒**：Key 只在创建时完整展示一次，请妥善保管。一个 Key 只能访问绑定的助手。

### Step 3 · 验证接口连通性

```bash
# 获取助手信息，验证 Key 是否有效
curl https://know.jitword.com/open/v1/info \
  -H "Authorization: Bearer jk-xxxxxxxxxxxxxxxx"
```

返回 `200` 及助手信息则表示 Key 有效，可以继续下一步。

### Step 4 · 发起流式对话

```bash
curl -X POST https://know.jitword.com/open/v1/chat \
  -H "Authorization: Bearer jk-xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{"message":"产品有哪些核心功能？"}' \
  --no-buffer
```

你将收到 SSE 流式响应，内容实时推送。

### Step 5 · 嵌入你的产品

复制下方 Widget 代码，粘贴到你的网页 `</body>` 标签前：

```html
<script>
  window.JitMindConfig = {
    assistantId: 'your-assistant-id',
    token:       'jk-xxxxxxxxxxxxxxxx',
    baseUrl:     'https://know.jitword.com',
    btnLabel:    '智能助手',
    btnColor:    '#165DFF'
  }
</script>
<script src="https://know.jitword.com/know/embed.js"></script>
```

**完成！** 你的网页右下角会出现一个 AI 智能助手悬浮按钮。🎉

---

## 📦 嵌入式 Widget 接入

### 悬浮气泡 Widget

最简单的接入方式，复制以下代码粘贴到 `</body>` 前，**一行代码**让网页拥有 AI 助手：

```html
<script>
  window.JitMindConfig = {
    assistantId: 'your-assistant-id',  // 必填：AI 助手 ID
    token:       'jk-xxxxxxxxxxxxxxxx', // 必填：API Key
    baseUrl:     'https://know.jitword.com', // 可选：私有化部署时需指定
    btnLabel:    '智能助手',            // 可选：悬浮按钮文案
    btnColor:    '#6366F1',             // 可选：按钮颜色（CSS 颜色值）
    theme:       'light',               // 可选：'light' | 'dark'
    position:    'bottom-right',        // 可选：悬浮按钮位置
    width:       380,                   // 可选：面板宽度（px）
    height:      600                    // 可选：面板高度（px）
  }
</script>
<script src="https://know.jitword.com/know/embed.js"></script>
```

**效果预览：**



### iframe 嵌入

适合需要将助手嵌入页面特定区域的场景：

```html
<iframe
  src="https://know.jitword.com/know/embed/{assistantId}?key=jk-xxxxxxxxxxxxxxxx&theme=light"
  width="400"
  height="600"
  style="border:none; border-radius:16px; box-shadow:0 4px 24px rgba(0,0,0,0.12)"
  allow="clipboard-write"
></iframe>
```

将 `{assistantId}` 和 `jk-xxx` 替换为你的真实值即可。

> **适用场景**：帮助中心页面、产品详情页的 AI 问答区、管理后台等固定位置嵌入。

### JitMindConfig 参数说明

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
|--------|------|:----:|--------|------|
| `assistantId` | `string` | ✅ 必填 | — | AI 助手的唯一 ID |
| `token` | `string` | ✅ 必填 | — | API Key，格式为 `jk-xxx` |
| `baseUrl` | `string` | 可选 | script origin | API 服务地址，**私有化部署时必须指定** |
| `theme` | `'light' \| 'dark'` | 可选 | `'light'` | 界面主题，浅色或深色 |
| `position` | `'bottom-right' \| 'bottom-left'` | 可选 | `'bottom-right'` | 悬浮按钮位置 |
| `btnColor` | `string` | 可选 | `'#6366F1'` | 悬浮按钮颜色（CSS 颜色值） |
| `btnLabel` | `string` | 可选 | `'智能助手'` | 悬浮按钮文案 |
| `width` | `number` | 可选 | `380` | 面板宽度（px，PC 端） |
| `height` | `number` | 可选 | `600` | 面板高度（px，PC 端） |

---

## 📡 API 参考文档

**Base URL：** `https://know.jitword.com/open/v1`

> 私有化部署时将 `https://know.jitword.com` 替换为你的服务域名。

### 鉴权方式

所有 API 请求均需在 HTTP Header 中携带 API Key：

```
Authorization: Bearer jk-xxxxxxxxxxxxxxxx
```

---

### `GET /info` · 获取助手信息

获取当前 API Key 绑定的助手信息，可用于初始化欢迎语、助手名称展示等。

**请求示例：**

```bash
curl https://know.jitword.com/open/v1/info \
  -H "Authorization: Bearer jk-xxxxxxxxxxxxxxxx"
```

**响应示例（200 OK）：**

```json
{
  "id": "asst_abc123",
  "name": "产品知识库助手",
  "description": "负责解答产品相关问题",
  "knowledge_base": "产品知识库",
  "model": "gpt-4o",
  "welcomeMessage": "你好！我是产品助手，有什么可以帮你？",
  "suggested_questions": [
    "产品有哪些核心功能？",
    "如何快速上手？",
    "支持哪些文件格式？"
  ]
}
```

**响应字段说明：**

| 字段 | 类型 | 说明 |
|------|------|------|
| `id` | `string` | 助手唯一 ID |
| `name` | `string` | 助手名称 |
| `description` | `string` | 助手描述 |
| `knowledge_base` | `string` | 绑定的知识库名称 |
| `model` | `string` | 使用的底层 AI 模型 |
| `welcomeMessage` | `string` | 欢迎语，可用于初始化 UI |
| `suggested_questions` | `string[]` | 推荐问题列表 |

---

### `POST /chat` · 发起流式对话（SSE）

向 AI 助手发送消息，获取 **SSE 流式回复**。支持多轮对话上下文，回复内容包含 Citations 知识来源引用。

**请求 Headers：**

```
Authorization: Bearer jk-xxxxxxxxxxxxxxxx
Content-Type: application/json
Accept: text/event-stream
```

**请求 Body：**

```json
{
  "message": "如何申请退款？",
  "conversationId": "conv_xxx"
}
```

**请求参数说明：**

| 参数 | 类型 | 必填 | 说明 |
|------|------|:----:|------|
| `message` | `string` | ✅ 必填 | 用户发送的消息，最大 8000 字符 |
| `conversationId` | `string` | 可选 | 续接多轮对话，不传则创建新会话 |

**响应（SSE 流式）：**

```
event: conversation_meta
data: {"conversation_id":"conv_a1b2c3d4"}

event: block_start
data: {}

event: block_delta
data: {"delta":"根据退款政策，您可以"}

event: block_delta
data: {"delta":"在购买后 7 天内申请退款..."}

event: block_replace
data: {"blocks":[{"type":"text","content":"根据退款政策，您可以在购买后 7 天内申请退款。\n\n申请步骤：\n1. 登录账户\n2. 进入订单详情\n3. 点击「申请退款」","citations":[{"title":"退款政策","source":"用户协议.pdf","page":3,"excerpt":"消费者可在购买后7个自然日内..."}]}]}

data: [DONE]
```

---

### SSE 事件说明

| 事件名 | `data` 字段 | 说明 |
|--------|-------------|------|
| `conversation_meta` | `{ conversation_id }` | 返回对话 ID，**保存此 ID** 用于续接多轮对话 |
| `block_start` | — | 新内容块开始，可用于显示 loading 动画 |
| `block_delta` | `{ delta }` | **流式增量文本**，每帧追加到展示区域（打字机效果） |
| `block_replace` | `{ blocks[0].content, blocks[0].citations }` | **完整最终内容**，含 Citations 引用，用于替换流式展示结果 |
| `[DONE]` | — | 流结束标志，关闭连接 |

**处理建议：**

```
监听 block_delta  → 实时追加文本，实现打字机效果
监听 block_replace → 用完整内容替换（处理 Markdown 格式化）
监听 [DONE]       → 关闭连接，隐藏 loading
保存 conversation_id → 用于下一轮对话的 conversationId 参数
```

**Citations 引用溯源字段结构：**

```json
"citations": [
  {
    "title": "退款政策",
    "source": "用户协议.pdf",
    "page": 3,
    "excerpt": "消费者可在购买后7个自然日内申请退款..."
  }
]
```

> 💡 **Citations 是 JitKnow 的核心差异化能力**：每个回答都标注了知识来源的文档名、页码和原文片段，帮助用户验证答案可靠性，大幅提升信任度。

---

## 💻 多语言代码示例

### cURL

```bash
# ── 1. 获取助手信息 ──────────────────────────────────────────
curl https://know.jitword.com/open/v1/info \
  -H "Authorization: Bearer jk-xxxxxxxxxxxxxxxx"

# ── 2. 发起流式对话（新会话）────────────────────────────────
curl -X POST https://know.jitword.com/open/v1/chat \
  -H "Authorization: Bearer jk-xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{"message":"产品有哪些核心功能？"}' \
  --no-buffer

# ── 3. 多轮对话（续接上一轮）────────────────────────────────
curl -X POST https://know.jitword.com/open/v1/chat \
  -H "Authorization: Bearer jk-xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{"message":"能详细说说第一点吗？","conversationId":"conv_a1b2c3d4"}' \
  --no-buffer
```

---

### JavaScript

```javascript
// JitKnow SSE 流式对话 - JavaScript / TypeScript 示例

const API_KEY  = 'jk-xxxxxxxxxxxxxxxx'
const BASE_URL = 'https://know.jitword.com/open/v1'

/**
 * 向 AI 助手发送消息，流式输出到页面
 * @param {string} message - 用户消息
 * @param {string} [conversationId] - 多轮对话 ID（可选）
 * @param {function} [onDelta] - 每收到增量文本时的回调
 * @returns {Promise<string>} 返回最终完整内容
 */
async function askAssistant(message, conversationId, onDelta) {
  const response = await fetch(`${BASE_URL}/chat`, {
    method: 'POST',
    headers: {
      'Authorization': `Bearer ${API_KEY}`,
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({ message, conversationId })
  })

  if (!response.ok) {
    const err = await response.json()
    throw new Error(`API Error ${response.status}: ${err?.error?.message}`)
  }

  const reader      = response.body.getReader()
  const decoder     = new TextDecoder()
  let buffer        = ''
  let currentEvent  = ''
  let finalContent  = ''

  while (true) {
    const { done, value } = await reader.read()
    if (done) break

    buffer += decoder.decode(value, { stream: true })
    const lines = buffer.split('\n')
    buffer = lines.pop() || ''

    for (const line of lines) {
      // 解析事件类型行
      if (line.startsWith('event: ')) {
        currentEvent = line.slice(7).trim()
        continue
      }
      // 空行 = 事件结束
      if (!line.trim()) { currentEvent = ''; continue }
      // 跳过非 data 行
      if (!line.startsWith('data: ')) continue

      const raw = line.slice(6).trim()
      if (!raw || raw === '[DONE]') continue

      const data = JSON.parse(raw)

      if (currentEvent === 'block_delta' && data.delta) {
        // 流式增量：追加到 UI（打字机效果）
        onDelta?.(data.delta)
      }

      if (currentEvent === 'block_replace' && data.blocks?.[0]) {
        // 最终完整内容（含 Markdown 格式化和 Citations）
        finalContent = data.blocks[0].content
        const citations = data.blocks[0].citations || []
        // 可在此处理 Citations 引用展示
        console.log('引用来源:', citations)
      }
    }
  }

  return finalContent
}

// ── 使用示例 ────────────────────────────────────────────────

const outputEl = document.getElementById('output')

askAssistant(
  '产品有哪些核心功能？',
  undefined,              // 新会话，不传 conversationId
  (delta) => {            // 实时追加文本
    outputEl.textContent += delta
  }
).then(finalContent => {
  // 用最终格式化内容替换流式结果
  outputEl.innerHTML = markdownToHtml(finalContent) // 使用你的 Markdown 渲染库
})
```

---

### Python

```python
# JitKnow SSE 流式对话 - Python 示例
# 依赖：pip install requests

import requests
import json

API_KEY  = "jk-xxxxxxxxxxxxxxxx"
BASE_URL = "https://know.jitword.com/open/v1"
HEADERS  = {"Authorization": f"Bearer {API_KEY}"}


def get_info() -> dict:
    """获取助手信息"""
    resp = requests.get(f"{BASE_URL}/info", headers=HEADERS)
    resp.raise_for_status()
    return resp.json()


def chat_stream(message: str, conversation_id: str = None) -> str:
    """
    发起 SSE 流式对话
    
    :param message: 用户消息
    :param conversation_id: 多轮对话 ID（可选）
    :return: 最终完整回复内容
    """
    body = {"message": message}
    if conversation_id:
        body["conversationId"] = conversation_id

    final_content = ""
    current_event = ""

    with requests.post(
        f"{BASE_URL}/chat",
        headers={**HEADERS, "Content-Type": "application/json"},
        json=body,
        stream=True
    ) as resp:
        resp.raise_for_status()

        for line in resp.iter_lines(decode_unicode=True):
            if line.startswith("event: "):
                current_event = line[7:].strip()

            elif line.startswith("data: "):
                raw = line[6:].strip()
                if not raw or raw == "[DONE]":
                    continue

                data = json.loads(raw)

                if current_event == "block_delta" and "delta" in data:
                    # 实时打印增量文本（打字机效果）
                    print(data["delta"], end="", flush=True)

                elif current_event == "block_replace" and "blocks" in data:
                    # 获取最终完整内容
                    block = data["blocks"][0]
                    final_content = block.get("content", "")
                    citations = block.get("citations", [])
                    if citations:
                        print("\n\n📚 引用来源：")
                        for c in citations:
                            print(f"  - {c['title']} ({c['source']}, 第{c.get('page','-')}页)")

            elif not line:
                current_event = ""

    print()  # 换行
    return final_content


# ── 使用示例 ────────────────────────────────────────────────

if __name__ == "__main__":
    # 获取助手信息
    info = get_info()
    print(f"助手名称：{info['name']}")
    print(f"欢迎语：{info['welcomeMessage']}\n")

    # 第一轮对话
    print("用户：产品有哪些核心功能？\nAI：", end="")
    chat_stream("产品有哪些核心功能？")

    # 多轮对话（需要保存 conversation_id，此处为示例）
    # conv_id = "conv_a1b2c3d4"  # 从 conversation_meta 事件获取
    # chat_stream("能详细说说第一点吗？", conversation_id=conv_id)
```

---

## 🔐 安全与限流

JitKnow 开放 API 采用**三层安全防护体系**，保障你的服务安全稳定：

### 第一层：API Key 权限隔离

- 每个 API Key **只能访问创建时绑定的单个助手**，无法越权访问其他助手数据
- Key 泄露后可立即在控制台**禁用或删除**，不影响其他 Key 和助手
- Key 不携带任何平台用户身份，调用方的用户体系自行管理

**Key 生命周期管理：**

```
创建 Key → [启用中] → 禁用 → [已禁用] → 重新启用
                   ↓
                 删除（不可恢复）
```

### 第二层：IP 白名单（可选）

为 Key 配置允许访问的来源 IP 列表，非白名单 IP 的请求直接拒绝（`HTTP 403`）。

- 支持精确 IP：`192.168.1.100`
- 支持 CIDR 段：`10.0.0.0/8`
- 最多配置 20 条规则
- 留空则不限制 IP（适合前端直接调用场景）

> 💡 **最佳实践**：服务端调用时配置 IP 白名单；前端直接调用时配合日配额限制。

### 第三层：调用频次控制

| 配额类型 | 控制粒度 | 超额响应 | 重置时机 |
|----------|----------|----------|----------|
| **RPM 速率限流** | 每分钟请求次数 | `HTTP 429` | 滑动窗口，实时重置 |
| **日调用配额** | 每日最大调用次数 | `HTTP 429` | 每天 00:00（UTC+8）自动重置 |
| **Key 过期时间** | 有效期截止日期 | `HTTP 401` | 手动在控制台延期 |

### 调用日志与审计

每次 API 调用均记录详细日志：

| 日志字段 | 说明 |
|----------|------|
| 请求时间 | 精确到毫秒 |
| 来源 IP | 调用方 IP 地址 |
| Key 名称 | 便于识别来源系统 |
| 耗时 | 首字节时间 + 总耗时 |
| Token 用量 | prompt / completion / total |
| 状态 | 成功 / 失败（含错误码） |

---

## 🚨 错误码参考

所有错误响应格式统一为：

```json
{
  "error": {
    "code": "rate_limit_exceeded",
    "message": "您的 API Key 已超过每分钟调用限制（20次/分钟），请稍后重试。",
    "retry_after": 30
  }
}
```

**完整错误码列表：**

| HTTP 状态码 | `error.code` | 说明 | 处理建议 |
|:-----------:|--------------|------|----------|
| `401` | `invalid_api_key` | API Key 无效或已被删除 | 检查 Key 是否正确 |
| `401` | `api_key_expired` | API Key 已过期 | 在控制台重新激活或创建新 Key |
| `403` | `ip_not_allowed` | 请求 IP 不在白名单 | 检查服务器出口 IP 配置 |
| `403` | `assistant_disabled` | 助手已被禁用 | 在控制台重新启用助手 |
| `422` | `query_too_long` | 输入内容超过 8000 字符限制 | 缩短输入内容 |
| `429` | `rate_limit_exceeded` | 触发 RPM 速率限制 | 等待 `retry_after` 秒后重试 |
| `429` | `daily_quota_exceeded` | 今日调用次数超限 | 等待次日 00:00 自动重置 |
| `500` | `model_error` | 底层 AI 模型调用失败 | 稍后重试，或联系技术支持 |
| `503` | `service_unavailable` | 服务暂时不可用 | 等待服务恢复，建议实现重试机制 |

**建议的错误处理逻辑：**

```javascript
async function callWithRetry(fn, maxRetries = 3) {
  for (let attempt = 0; attempt < maxRetries; attempt++) {
    try {
      return await fn()
    } catch (err) {
      if (err.status === 429) {
        const retryAfter = err.retryAfter || 30
        await sleep(retryAfter * 1000)
        continue
      }
      if (err.status === 503 && attempt < maxRetries - 1) {
        await sleep(2 ** attempt * 1000) // 指数退避
        continue
      }
      throw err
    }
  }
}
```

---

## ❓ 常见问题 FAQ

<details>
<summary><strong>Q：API Key 泄露了怎么办？</strong></summary>

**立即**进入 JitKnow 控制台 → 助手详情 → API 接入 Tab → 找到该 Key → 点击「禁用」或「删除」。

Key 被禁用后，所有使用该 Key 的请求均返回 `401`，不影响其他 Key 和助手的正常运行。建议重新创建一个新 Key 并更新你的服务配置。

</details>

<details>
<summary><strong>Q：支持私有化部署后自托管 API 吗？</strong></summary>

完全支持。私有化部署的 JitKnow 实例与 SaaS 版本功能完全一致，开放 API 同样可用。

只需将所有 API 调用地址改为你的私有服务域名：
- Widget：设置 `baseUrl: 'https://your-domain.com'`
- API 调用：将 `https://know.jitword.com` 替换为 `https://your-domain.com`

</details>

<details>
<summary><strong>Q：/chat 接口只支持流式吗？如何获取完整内容？</strong></summary>

`/chat` 接口统一使用 SSE 流式输出，提供最佳用户体验。

如果你的场景需要等待完整回答（如批量处理、服务端生成），请监听 **`block_replace`** 事件：

```javascript
if (currentEvent === 'block_replace') {
  const finalContent = data.blocks[0].content  // 完整最终内容
  const citations    = data.blocks[0].citations // Citations 引用
  // 此处关闭连接，处理完整内容
}
```

</details>

<details>
<summary><strong>Q：Citations 引用溯源是如何工作的？</strong></summary>

JitKnow 基于 **RAG（检索增强生成）** 技术，每次回答都会从知识库中检索相关文档片段作为参考依据。

`block_replace` 事件的 `blocks[0].citations` 字段包含每条引用的：
- `title`：引用文档名称
- `source`：原始文件名
- `page`：所在页码
- `excerpt`：原文片段

建议在 UI 中展示「参考来源」折叠面板，大幅提升用户对 AI 回答的信任度。

</details>

<details>
<summary><strong>Q：如何更换底层 AI 模型（GPT-4o / Claude / Deepseek）？</strong></summary>

底层模型在 JitKnow 控制台「**助手设置**」中配置，支持：
- GPT-4o、GPT-4 Turbo
- Claude 3.5 Sonnet、Claude 3 Opus
- Gemini Pro
- Deepseek V3
- 自定义 API 兼容模型（OpenAI 协议）

修改助手的模型配置后，API 调用会**自动使用新模型**，无需更改任何接入代码。

</details>

<details>
<summary><strong>Q：调用量超出配额后会怎样？如何处理？</strong></summary>

超出 RPM 限流或日调用配额后，接口返回 `HTTP 429 Too Many Requests`：

```json
{
  "error": {
    "code": "rate_limit_exceeded",
    "message": "请求频率超限，请稍后再试",
    "retry_after": 30
  }
}
```

**建议处理方式：**
- 前端：展示友好提示「服务繁忙，请稍后再试」
- 后端：实现指数退避重试机制，等待 `retry_after` 秒后重试
- 日配额：每天 00:00（UTC+8）自动重置

</details>

<details>
<summary><strong>Q：多轮对话如何实现？conversationId 从哪里获取？</strong></summary>

多轮对话的关键是 `conversationId`：

**第一轮**（新会话）：不传 `conversationId`，API 返回的第一个 SSE 事件 `conversation_meta` 中包含 `conversation_id`：

```
event: conversation_meta
data: {"conversation_id":"conv_a1b2c3d4"}
```

**后续轮次**：在 request body 中传入 `conversationId: "conv_a1b2c3d4"` 即可续接上下文。

> API 后端会维护最近 10 轮对话历史（可在助手设置中调整）。

</details>

---

## 📞 联系我们

| 渠道 | 联系方式 |
|------|----------|
| 📧 邮箱 | flowmix@163.com |
| 💬 微信 | cxzk_168 |
| 🌐 官网 | [know.jitword.com](https://know.jitword.com) |
| 🏢 公司 | 重庆橙讯智科科技有限公司 |

> 遇到接入问题？添加微信 **cxzk_168** 获得 1v1 技术协助。

---

<div align="center">

**[注册账号，立即获取 API Key →](https://know.jitword.com/know/login)**

© 2026 JitKnow · 重庆橙讯智科科技有限公司 · [隐私政策](https://jitword.com) · [服务条款](https://jitword.com)

*用一行代码，给你的产品装上 AI 知识大脑。*

</div>
