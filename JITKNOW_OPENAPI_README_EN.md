<div align="center">

<img src="https://know.jitword.com/public/uploads/know-logo_19d18ea166a.png" width="120" alt="JitKnow Logo" style="border-radius:16px"/>

# JitKnow API Open Platform

**🌐 Language · 语言版本 · 言語**

[![中文](https://img.shields.io/badge/中文-查看-6B7280?style=flat-square)](./JITKNOW_OPENAPI_README.md)
[![English](https://img.shields.io/badge/English-Current-165DFF?style=flat-square)](./JITKNOW_OPENAPI_README_EN.md)
[![日本語](https://img.shields.io/badge/日本語-查看-6B7280?style=flat-square)](./JITKNOW_OPENAPI_README_JA.md)

**Enterprise AI Knowledge Base · Developer Documentation**

[![API Version](https://img.shields.io/badge/API-v1-165DFF?style=flat-square&logo=swagger)](https://know.jitword.com)
[![SSE Stream](https://img.shields.io/badge/Stream-SSE-10B981?style=flat-square&logo=lightning)](https://know.jitword.com)
[![Auth](https://img.shields.io/badge/Auth-Bearer_Token-8B5CF6?style=flat-square&logo=shield)](https://know.jitword.com)
[![License](https://img.shields.io/badge/License-Commercial-F59E0B?style=flat-square)](https://know.jitword.com)
[![Contact](https://img.shields.io/badge/WeChat-cxzk__168-07C160?style=flat-square&logo=wechat)](https://know.jitword.com)

> 🚀 **Integrate in 5 minutes** — give your website, app, or internal system a dedicated AI knowledge base Q&A capability.  
> Embeddable Widget · RESTful Chat API · SSE Streaming · Citations Source Tracing

[Get Started](https://know.jitword.com/know/login) · [Online Docs](https://jitword.com) · [Technical Support](https://know.jitword.com)

</div>

---

## Table of Contents

- [✨ Product Overview](#-product-overview)
- [🗺️ Capability Map](#️-capability-map)
- [⚡ Quick Start (5 Steps)](#-quick-start-5-steps)
- [📦 Embeddable Widget Integration](#-embeddable-widget-integration)
  - [Floating Bubble Widget](#floating-bubble-widget)
  - [iframe Embed](#iframe-embed)
  - [JitMindConfig Parameter Reference](#jitmindconfig-parameter-reference)
- [📡 API Reference](#-api-reference)
  - [Authentication](#authentication)
  - [GET /info · Get Assistant Info](#get-info--get-assistant-info)
  - [POST /chat · Start Streaming Chat](#post-chat--start-streaming-chat-sse)
  - [SSE Event Reference](#sse-event-reference)
- [💻 Code Examples](#-code-examples)
  - [cURL](#curl)
  - [JavaScript](#javascript)
  - [Python](#python)
- [🔐 Security & Rate Limiting](#-security--rate-limiting)
- [🚨 Error Code Reference](#-error-code-reference)
- [❓ FAQ](#-faq)
- [📞 Contact Us](#-contact-us)

---

## ✨ Product Overview

JitKnow is an enterprise-grade **AI intelligent knowledge base platform** that transforms documents in 20+ formats — PDF, Word, Excel, web pages and more — into a dedicated AI knowledge base using RAG (Retrieval-Augmented Generation) for accurate Q&A.

The **JitKnow Open Platform** exposes this AI capability as an API for third-party developers. Typical use cases include:

| Scenario | Description |
|----------|-------------|
| 🌐 **Website AI Customer Service** | Embed a product-manual-powered AI assistant into your website to replace manual support |
| 💼 **Enterprise Internal Tools** | Integrate HR / Legal / Tech doc assistants into OA systems, DingTalk, or Feishu |
| 🤖 **In-App AI Q&A** | Deliver AI knowledge base Q&A in mobile apps via API |
| ⚙️ **SaaS Product Enhancement** | Embed an AI Q&A module into your own SaaS product to improve user experience |

---

## 🗺️ Capability Map

```
┌─────────────────────────────────────────────────────────────┐
│                  JitKnow Open Platform                       │
├─────────────────┬─────────────────┬─────────────────────────┤
│  📦 Embed Widget │  📡 Chat API    │  🔐 Security & Control  │
├─────────────────┼─────────────────┼─────────────────────────┤
│ Floating Bubble  │ GET  /info      │ API Key Permission      │
│ iframe Embed    │ POST /chat (SSE)│ IP Allowlist Control    │
│ Dark / Light    │ Multi-turn ctx  │ RPM Rate Limiting       │
│ Custom color    │ Citations       │ Daily Call Quota        │
│ 1-line setup    │ Real-time stream│ Key Expiry Management   │
└─────────────────┴─────────────────┴─────────────────────────┘
```

**Competitive Comparison:**

| Capability | JitKnow | Dify | Coze |
|------------|:-------:|:----:|:----:|
| API Key Management (multi-key + quota) | ✅ | ✅ | ✅ |
| SSE Streaming Output | ✅ | ✅ | ✅ |
| Multi-turn Conversation `conversationId` | ✅ | ✅ | ✅ |
| **Citations Source Tracing** | ✅ **Key Differentiator** | ✅ | ⚠️ Limited |
| IP Allowlist | ✅ | ⚠️ Enterprise only | ❌ |
| Embeddable Widget (embed.js) | ✅ | ✅ | ✅ |
| Self-hosted API after private deployment | ✅ | ✅ | ❌ |
| Native enterprise knowledge base binding | ✅ **Key Differentiator** | ⚠️ Generic | ⚠️ Generic |

---

## ⚡ Quick Start (5 Steps)

### Step 1 · Register and Create an AI Assistant

Visit [JitKnow Platform](https://know.jitword.com/know/login) to register, create an AI assistant, upload your product docs, FAQs, and knowledge articles to build a dedicated knowledge base.

### Step 2 · Get an API Key

Go to **Assistant Detail → API Integration Tab → Create API Key**, and record:

- `assistantId`: the unique ID of your assistant
- API Key: in the format `jk-xxxxxxxxxxxxxxxx`

> ⚠️ **Security Notice**: The full Key is only shown once at creation time — store it safely. Each Key can only access the assistant it was created for.

### Step 3 · Verify Connectivity

```bash
# Fetch assistant info to verify the Key is valid
curl https://know.jitword.com/open/v1/info \
  -H "Authorization: Bearer jk-xxxxxxxxxxxxxxxx"
```

A `200` response with assistant details confirms the Key is active.

### Step 4 · Send a Streaming Chat Request

```bash
curl -X POST https://know.jitword.com/open/v1/chat \
  -H "Authorization: Bearer jk-xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{"message":"What are the core features of the product?"}' \
  --no-buffer
```

You will receive a real-time SSE streaming response.

### Step 5 · Embed into Your Product

Paste the Widget snippet before your `</body>` tag:

```html
<script>
  window.JitMindConfig = {
    assistantId: 'your-assistant-id',
    token:       'jk-xxxxxxxxxxxxxxxx',
    baseUrl:     'https://know.jitword.com',
    btnLabel:    'AI Assistant',
    btnColor:    '#165DFF'
  }
</script>
<script src="https://know.jitword.com/know/embed.js"></script>
```

**Done!** A floating AI assistant button will appear in the bottom-right corner of your page. 🎉

---

## 📦 Embeddable Widget Integration

### Floating Bubble Widget

The simplest integration — paste one snippet before `</body>` and your page instantly gains an AI assistant:

```html
<script>
  window.JitMindConfig = {
    assistantId: 'your-assistant-id',   // Required: AI assistant ID
    token:       'jk-xxxxxxxxxxxxxxxx',  // Required: API Key
    baseUrl:     'https://know.jitword.com', // Optional: required for self-hosted deployments
    btnLabel:    'AI Assistant',         // Optional: button label text
    btnColor:    '#6366F1',              // Optional: button color (any CSS color)
    theme:       'light',               // Optional: 'light' | 'dark'
    position:    'bottom-right',        // Optional: button position
    width:       380,                   // Optional: panel width (px)
    height:      600                    // Optional: panel height (px)
  }
</script>
<script src="https://know.jitword.com/know/embed.js"></script>
```

**Preview:**

<img src="./widget.png" />

### iframe Embed

Ideal for embedding the assistant in a specific section of a page:

```html
<iframe
  src="https://know.jitword.com/know/embed/{assistantId}?key=jk-xxxxxxxxxxxxxxxx&theme=light"
  width="400"
  height="600"
  style="border:none; border-radius:16px; box-shadow:0 4px 24px rgba(0,0,0,0.12)"
  allow="clipboard-write"
></iframe>
```

Replace `{assistantId}` and `jk-xxx` with your actual values.

> **Best for**: Help center pages, product detail pages with inline AI Q&A, admin dashboards.

### JitMindConfig Parameter Reference

| Parameter | Type | Required | Default | Description |
|-----------|------|:--------:|---------|-------------|
| `assistantId` | `string` | ✅ Yes | — | Unique AI assistant ID |
| `token` | `string` | ✅ Yes | — | API Key in `jk-xxx` format |
| `baseUrl` | `string` | Optional | script origin | API server URL; **required for self-hosted deployments** |
| `theme` | `'light' \| 'dark'` | Optional | `'light'` | UI theme |
| `position` | `'bottom-right' \| 'bottom-left'` | Optional | `'bottom-right'` | Floating button position |
| `btnColor` | `string` | Optional | `'#6366F1'` | Button color (CSS color value) |
| `btnLabel` | `string` | Optional | `'AI Assistant'` | Button label text |
| `width` | `number` | Optional | `380` | Panel width in px (desktop) |
| `height` | `number` | Optional | `600` | Panel height in px (desktop) |

---

## 📡 API Reference

**Base URL:** `https://know.jitword.com/open/v1`

> For self-hosted deployments, replace `https://know.jitword.com` with your service domain.

### Authentication

All API requests must include the API Key in the HTTP header:

```
Authorization: Bearer jk-xxxxxxxxxxxxxxxx
```

---

### `GET /info` · Get Assistant Info

Returns the assistant details bound to the current API Key. Use this to initialize the welcome message or display the assistant's name.

**Request:**

```bash
curl https://know.jitword.com/open/v1/info \
  -H "Authorization: Bearer jk-xxxxxxxxxxxxxxxx"
```

**Response (200 OK):**

```json
{
  "id": "asst_abc123",
  "name": "Product Knowledge Assistant",
  "description": "Answers product-related questions",
  "knowledge_base": "Product Knowledge Base",
  "model": "gpt-4o",
  "welcomeMessage": "Hi! I'm your product assistant. How can I help you?",
  "suggested_questions": [
    "What are the core features?",
    "How do I get started?",
    "What file formats are supported?"
  ]
}
```

**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `id` | `string` | Unique assistant ID |
| `name` | `string` | Assistant name |
| `description` | `string` | Assistant description |
| `knowledge_base` | `string` | Bound knowledge base name |
| `model` | `string` | Underlying AI model in use |
| `welcomeMessage` | `string` | Welcome message for UI initialization |
| `suggested_questions` | `string[]` | Suggested question list |

---

### `POST /chat` · Start Streaming Chat (SSE)

Send a message to the AI assistant and receive an **SSE streaming reply**. Supports multi-turn conversation context and returns Citations knowledge source references.

**Request Headers:**

```
Authorization: Bearer jk-xxxxxxxxxxxxxxxx
Content-Type: application/json
Accept: text/event-stream
```

**Request Body:**

```json
{
  "message": "How do I request a refund?",
  "conversationId": "conv_xxx"
}
```

**Request Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|:--------:|-------------|
| `message` | `string` | ✅ Yes | User message, max 8000 characters |
| `conversationId` | `string` | Optional | Continue a multi-turn conversation; omit to start a new one |

**Response (SSE stream):**

```
event: conversation_meta
data: {"conversation_id":"conv_a1b2c3d4"}

event: block_start
data: {}

event: block_delta
data: {"delta":"Based on our refund policy, you can "}

event: block_delta
data: {"delta":"submit a refund request within 7 days of purchase..."}

event: block_replace
data: {"blocks":[{"type":"text","content":"Based on our refund policy, you can submit a refund request within 7 days of purchase.\n\nSteps:\n1. Log in to your account\n2. Go to order details\n3. Click 'Request Refund'","citations":[{"title":"Refund Policy","source":"Terms of Service.pdf","page":3,"excerpt":"Customers may request a refund within 7 calendar days..."}]}]}

data: [DONE]
```

---

### SSE Event Reference

| Event Name | `data` Fields | Description |
|------------|---------------|-------------|
| `conversation_meta` | `{ conversation_id }` | Returns the conversation ID — **save this** for multi-turn follow-ups |
| `block_start` | — | A new content block is beginning; show a loading indicator |
| `block_delta` | `{ delta }` | **Incremental streaming text** — append to the display area (typewriter effect) |
| `block_replace` | `{ blocks[0].content, blocks[0].citations }` | **Final complete content** with Citations — replace the streamed text |
| `[DONE]` | — | Stream end signal — close the connection |

**Recommended Handling:**

```
Listen for block_delta   → Append text incrementally (typewriter effect)
Listen for block_replace → Replace with final formatted content (Markdown)
Listen for [DONE]        → Close connection, hide loading indicator
Save conversation_id     → Pass as conversationId in the next turn
```

**Citations Field Structure:**

```json
"citations": [
  {
    "title": "Refund Policy",
    "source": "Terms of Service.pdf",
    "page": 3,
    "excerpt": "Customers may request a refund within 7 calendar days..."
  }
]
```

> 💡 **Citations is JitKnow's core differentiator**: every answer is annotated with its knowledge source — document name, page number, and the original excerpt — helping users verify answer reliability and significantly boosting trust.

---

## 💻 Code Examples

### cURL

```bash
# ── 1. Get assistant info ────────────────────────────────────
curl https://know.jitword.com/open/v1/info \
  -H "Authorization: Bearer jk-xxxxxxxxxxxxxxxx"

# ── 2. Start a streaming chat (new conversation) ─────────────
curl -X POST https://know.jitword.com/open/v1/chat \
  -H "Authorization: Bearer jk-xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{"message":"What are the core features of the product?"}' \
  --no-buffer

# ── 3. Continue a multi-turn conversation ────────────────────
curl -X POST https://know.jitword.com/open/v1/chat \
  -H "Authorization: Bearer jk-xxxxxxxxxxxxxxxx" \
  -H "Content-Type: application/json" \
  -d '{"message":"Can you elaborate on the first point?","conversationId":"conv_a1b2c3d4"}' \
  --no-buffer
```

---

### JavaScript

```javascript
// JitKnow SSE Streaming Chat - JavaScript / TypeScript Example

const API_KEY  = 'jk-xxxxxxxxxxxxxxxx'
const BASE_URL = 'https://know.jitword.com/open/v1'

/**
 * Send a message to the AI assistant with streaming output
 * @param {string} message - User message
 * @param {string} [conversationId] - Multi-turn conversation ID (optional)
 * @param {function} [onDelta] - Callback fired on each incremental text chunk
 * @returns {Promise<string>} Final complete content
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
      if (line.startsWith('event: ')) {
        currentEvent = line.slice(7).trim()
        continue
      }
      if (!line.trim()) { currentEvent = ''; continue }
      if (!line.startsWith('data: ')) continue

      const raw = line.slice(6).trim()
      if (!raw || raw === '[DONE]') continue

      const data = JSON.parse(raw)

      if (currentEvent === 'block_delta' && data.delta) {
        // Streaming increment: append to UI (typewriter effect)
        onDelta?.(data.delta)
      }

      if (currentEvent === 'block_replace' && data.blocks?.[0]) {
        // Final complete content with optional Citations
        finalContent = data.blocks[0].content
        const citations = data.blocks[0].citations || []
        console.log('Sources:', citations)
      }
    }
  }

  return finalContent
}

// ── Usage Example ────────────────────────────────────────────

const outputEl = document.getElementById('output')

askAssistant(
  'What are the core features of the product?',
  undefined,              // new conversation — no conversationId
  (delta) => {            // append each incremental chunk
    outputEl.textContent += delta
  }
).then(finalContent => {
  // Replace streamed text with final formatted content
  outputEl.innerHTML = markdownToHtml(finalContent) // use your Markdown renderer
})
```

---

### Python

```python
# JitKnow SSE Streaming Chat - Python Example
# Requires: pip install requests

import requests
import json

API_KEY  = "jk-xxxxxxxxxxxxxxxx"
BASE_URL = "https://know.jitword.com/open/v1"
HEADERS  = {"Authorization": f"Bearer {API_KEY}"}


def get_info() -> dict:
    """Fetch assistant information."""
    resp = requests.get(f"{BASE_URL}/info", headers=HEADERS)
    resp.raise_for_status()
    return resp.json()


def chat_stream(message: str, conversation_id: str = None) -> str:
    """
    Send a streaming chat request via SSE.

    :param message: User message
    :param conversation_id: Multi-turn conversation ID (optional)
    :return: Final complete reply content
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
                    # Print incremental text (typewriter effect)
                    print(data["delta"], end="", flush=True)

                elif current_event == "block_replace" and "blocks" in data:
                    block = data["blocks"][0]
                    final_content = block.get("content", "")
                    citations = block.get("citations", [])
                    if citations:
                        print("\n\n📚 Sources:")
                        for c in citations:
                            print(f"  - {c['title']} ({c['source']}, p.{c.get('page', '-')})")

            elif not line:
                current_event = ""

    print()  # newline
    return final_content


# ── Usage ────────────────────────────────────────────────────

if __name__ == "__main__":
    info = get_info()
    print(f"Assistant: {info['name']}")
    print(f"Welcome: {info['welcomeMessage']}\n")

    print("User: What are the core features?\nAI: ", end="")
    chat_stream("What are the core features of the product?")

    # Multi-turn conversation (save conversation_id from conversation_meta event)
    # conv_id = "conv_a1b2c3d4"
    # chat_stream("Can you elaborate on point one?", conversation_id=conv_id)
```

---

## 🔐 Security & Rate Limiting

JitKnow's Open API employs a **three-layer security model** to keep your service safe and stable.

### Layer 1: API Key Permission Isolation

- Each API Key can **only access the single assistant it was bound to** at creation; cross-assistant access is not possible
- A compromised Key can be **immediately disabled or deleted** from the console without affecting other Keys
- Keys carry no platform user identity; caller-side user management is entirely the developer's responsibility

**Key Lifecycle:**

```
Create Key → [Active] → Disable → [Disabled] → Re-enable
                     ↓
                   Delete (irreversible)
```

### Layer 2: IP Allowlist (Optional)

Configure the allowed source IP addresses for a Key; requests from non-allowlisted IPs are rejected with `HTTP 403`.

- Exact IPs: `192.168.1.100`
- CIDR ranges: `10.0.0.0/8`
- Up to 20 rules per Key
- Leave empty to allow all IPs (suitable for frontend direct calls)

> 💡 **Best Practice**: Configure IP allowlist for server-side calls; combine with daily quota limits for frontend direct calls.

### Layer 3: Call Rate Controls

| Quota Type | Scope | Over-limit Response | Reset |
|------------|-------|---------------------|-------|
| **RPM Rate Limit** | Requests per minute | `HTTP 429` | Sliding window, real-time |
| **Daily Call Quota** | Max daily calls | `HTTP 429` | Auto-reset at 00:00 (UTC+8) |
| **Key Expiry** | Valid-until date | `HTTP 401` | Manual renewal in console |

### Call Logs & Audit

Every API call is logged with full detail:

| Log Field | Description |
|-----------|-------------|
| Request Time | Millisecond precision |
| Source IP | Caller IP address |
| Key Name | Identifies the calling system |
| Latency | Time to first byte + total duration |
| Token Usage | prompt / completion / total |
| Status | Success / Failure (with error code) |

---

## 🚨 Error Code Reference

All error responses follow a unified format:

```json
{
  "error": {
    "code": "rate_limit_exceeded",
    "message": "Your API Key has exceeded the per-minute call limit (20 rpm). Please retry after 30 seconds.",
    "retry_after": 30
  }
}
```

**Complete Error Code Table:**

| HTTP Status | `error.code` | Description | Recommended Action |
|:-----------:|--------------|-------------|-------------------|
| `401` | `invalid_api_key` | API Key is invalid or has been deleted | Verify the Key value |
| `401` | `api_key_expired` | API Key has expired | Re-activate or create a new Key |
| `403` | `ip_not_allowed` | Request IP is not in the allowlist | Check server egress IP configuration |
| `403` | `assistant_disabled` | The assistant has been disabled | Re-enable the assistant in the console |
| `422` | `query_too_long` | Input exceeds the 8000-character limit | Shorten the input |
| `429` | `rate_limit_exceeded` | RPM rate limit triggered | Wait `retry_after` seconds and retry |
| `429` | `daily_quota_exceeded` | Daily call quota exhausted | Wait for auto-reset at 00:00 UTC+8 |
| `500` | `model_error` | Underlying AI model call failed | Retry later or contact support |
| `503` | `service_unavailable` | Service temporarily unavailable | Wait and implement retry with backoff |

**Recommended Error Handling:**

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
        await sleep(2 ** attempt * 1000) // exponential backoff
        continue
      }
      throw err
    }
  }
}
```

---

## ❓ FAQ

<details>
<summary><strong>Q: My API Key was leaked — what should I do?</strong></summary>

**Immediately** go to JitKnow Console → Assistant Detail → API Integration Tab → locate the Key → click **Disable** or **Delete**.

Once disabled, all requests using that Key return `401`. Other Keys and assistants are not affected. Create a new Key and update your service configuration.

</details>

<details>
<summary><strong>Q: Can I self-host the API after a private deployment?</strong></summary>

Absolutely. A self-hosted JitKnow instance is fully feature-equivalent to the SaaS version, and the Open API works the same way.

Simply replace all API call URLs with your private service domain:
- Widget: set `baseUrl: 'https://your-domain.com'`
- Direct API calls: replace `https://know.jitword.com` with `https://your-domain.com`

</details>

<details>
<summary><strong>Q: Is /chat streaming only? How do I get the complete response?</strong></summary>

The `/chat` endpoint uses SSE streaming for the best user experience.

If you need the complete response without streaming (e.g. batch processing, server-side generation), listen for the **`block_replace`** event:

```javascript
if (currentEvent === 'block_replace') {
  const finalContent = data.blocks[0].content  // complete final content
  const citations    = data.blocks[0].citations // Citations sources
  // Close connection and process the full content here
}
```

</details>

<details>
<summary><strong>Q: How does Citations source tracing work?</strong></summary>

JitKnow uses **RAG (Retrieval-Augmented Generation)**: every answer retrieves relevant document chunks from the knowledge base as supporting references.

The `block_replace` event's `blocks[0].citations` array contains:
- `title`: Reference document name
- `source`: Original filename
- `page`: Page number
- `excerpt`: Original text snippet

We recommend displaying a collapsible "Sources" panel in your UI — this significantly boosts user trust in AI-generated answers.

</details>

<details>
<summary><strong>Q: How do I switch the underlying AI model (GPT-4o / Claude / Deepseek)?</strong></summary>

The model is configured in the JitKnow console under **Assistant Settings**. Supported models include:
- GPT-4o, GPT-4 Turbo
- Claude 3.5 Sonnet, Claude 3 Opus
- Gemini Pro
- Deepseek V3
- Custom OpenAI-protocol-compatible models

After changing the model in Assistant Settings, API calls **automatically use the new model** — no code changes required.

</details>

<details>
<summary><strong>Q: What happens when the quota is exceeded? How should I handle it?</strong></summary>

Exceeding the RPM limit or daily quota returns `HTTP 429 Too Many Requests`:

```json
{
  "error": {
    "code": "rate_limit_exceeded",
    "message": "Request rate exceeded. Please try again later.",
    "retry_after": 30
  }
}
```

**Recommended handling:**
- Frontend: show a friendly message — "Service is busy, please try again shortly"
- Backend: implement exponential backoff retry, waiting `retry_after` seconds
- Daily quota: resets automatically at 00:00 UTC+8 each day

</details>

<details>
<summary><strong>Q: How do multi-turn conversations work? Where does conversationId come from?</strong></summary>

The key to multi-turn conversations is `conversationId`:

**First turn** (new conversation): omit `conversationId`. The first SSE event `conversation_meta` contains it:

```
event: conversation_meta
data: {"conversation_id":"conv_a1b2c3d4"}
```

**Subsequent turns**: pass `conversationId: "conv_a1b2c3d4"` in the request body to continue the context.

> The API backend maintains up to the last 10 conversation turns (configurable in Assistant Settings).

</details>

---

## 📞 Contact Us

| Channel | Details |
|---------|---------|
| 📧 Email | flowmix@163.com |
| 💬 WeChat | cxzk_168 |
| 🌐 Website | [know.jitword.com](https://know.jitword.com) |
| 🏢 Company | Chongqing Chengxun Zhike Technology Co., Ltd. |

> Having trouble with integration? Add WeChat **cxzk_168** for 1-on-1 technical support.

---

<div align="center">

**[Register Now and Get Your API Key →](https://know.jitword.com/know/login)**

© 2026 JitKnow 

*One line of code. Infinite AI knowledge.*

</div>
