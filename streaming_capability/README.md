# 🌊 Streaming Response Capability (`streaming_capability`)

This capability implements and demonstrates the **Streamed Message Action** (`type: streamed-message`) for real-time Server-Sent Events (SSE) streaming in SAP Joule.

---

## 🎯 Key Concepts Covered

1. **Server-Sent Events (SSE)** real-time data streaming into Joule UI.
2. **Mandatory Headers**:
   - `Accept: "text/event-stream"`
   - `Connection: "keep-alive"`
   - `Cache-Control: "no-cache"`
3. **JSON Response Chunk Referencing**:
   - Uses JSONPath expression `$.delta.content` to extract text from SSE JSON payloads: `data: {"delta":{"content":"text"}}`
4. **Plain Text Response Chunk Referencing**:
   - Uses root `$` to extract text from raw SSE payloads: `data: text`
5. **Automatic Aggregation**: Joule aggregates chunks in real-time and updates the context variable defined in `result_variable`.

---

## 📁 File Structure

- [`capability.sapdas.yaml`](file:///home/kiranftw/joule_ai/streaming_capability/capability.sapdas.yaml): Descriptor manifest defining `StreamingService` system alias.
- [`scenarios/stream_response.yaml`](file:///home/kiranftw/joule_ai/streaming_capability/scenarios/stream_response.yaml): Scenario trigger definition for streaming queries.
- [`functions/stream_response_function.yaml`](file:///home/kiranftw/joule_ai/streaming_capability/functions/stream_response_function.yaml): Dialog function implementing `type: streamed-message` for JSON and Plain Text streams.

---

## ⚡ Deployment & Testing

1. Configure `da.sapdas.yaml` to point to `./streaming_capability`:
   ```yaml
   schema_version: 1.4.0
   name: streaming_assistant
   capabilities:
     - type: local
       folder: ./streaming_capability
   ```

2. Compile and Deploy:
   ```bash
   joule lint ./streaming_capability
   joule compile ./streaming_capability
   joule deploy da.sapdas.yaml
   ```
