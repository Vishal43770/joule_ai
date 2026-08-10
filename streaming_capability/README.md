# Server-Sent Events (SSE) Streamed Messages (`streaming_capability`)

This capability demonstrates **Streamed Message Actions (`type: streamed-message`)** and **Live Token Response Streaming** in SAP Joule, based on pages 70–72 of the *Joule Development Guide*.

---

## 📁 File Structure

```text
streaming_capability/
├── capability.sapdas.yaml          # Capability metadata descriptor (v3.28.0)
├── README.md                       # This documentation file
├── functions/
│   └── stream_response_function.yaml # Dialog function executing SSE streamed response simulation
└── scenarios/
    └── stream_response.yaml        # Scenario defining slots and intent description for natural queries
```

---

## 💡 Key Architectural Concepts

### 1. Server-Sent Events (SSE) Streamed Messages (`type: streamed-message`)

Streamed messages deliver live AI response tokens chunk-by-chunk over Server-Sent Events (SSE):

```yaml
- type: streamed-message
  method: POST
  system_alias: StreamingService
  path: "/api/v1/stream/json"
  headers:
    Accept: "text/event-stream"
  response_chunk_ref: $.delta.content # Chunks extracted from SSE JSON payload
  result_variable: streamed_json_result
```

---

### 2. Natural Intent Matching

Scenario descriptions use natural language phrasing so users can ask questions naturally without typing technical keywords like *"stream"*:

```yaml
# scenarios/stream_response.yaml
description: Answer questions and provide information about quantum computing, artificial intelligence, technology topics, and general queries.
```

---

## 🛠 Joule CLI Commands

Run these commands inside `C:\Users\VISHAL\office\joule_ai`:

```powershell
# 1. Lint the capability
joule lint ./streaming_capability

# 2. Compile the capability
joule compile ./streaming_capability

# 3. Deploy the digital assistant
joule deploy da.sapdas.yaml

# 4. Launch the assistant
joule launch streaming_assistant
```

---

## 💬 Test Queries in Joule Chat

1. **`Tell me about quantum computing`** ➔ *Renders Streamed AI Response Card*
2. **`What is artificial intelligence?`** ➔ *Renders Markdown Text Stream*
