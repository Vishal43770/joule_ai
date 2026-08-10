# 🚀 SAP Joule AI Learning Capabilities Repository (`joule_ai`)

This repository contains modular, standalone SAP Joule extensibility capabilities (`schema_version: 3.28.0`) designed to test, verify, and master every core feature in the **Official SAP Joule Development Guide**.

---

## 📂 Capability Modules Index

| Capability Folder | Key Concept Covered | Guide Page Ref | Assistant Name |
|---|---|---|---|
| **[`sample_capability`](file:///c:/Users/VISHAL/office/joule_ai/sample_capability/README.md)** | **7 UI Message Variations**, Fiori Cards, Analytical Dashboard Cards, Likert Scale Feedback Loops | Pages 41–44, 165–180 | `weather_assistant` |
| **[`greeting_capability`](file:///c:/Users/VISHAL/office/joule_ai/greeting_capability/README.md)** | **Static Parameter Injection**, User Context (`$transient.user`), Custom Intent Matching | Page 47 | `greeting_assistant` |
| **[`context_capability`](file:///c:/Users/VISHAL/office/joule_ai/context_capability/README.md)** | **Capability Context Variables** (`$capability_context`), Target Parameter Passing, `$target_result` Context Updates | Pages 61–62 | `context_assistant` |
| **[`dependency_capability`](file:///c:/Users/VISHAL/office/joule_ai/dependency_capability/README.md)** | **Scenario Dependencies** (`sources:`), Mandatory Parameters (`optional: false`), Auto-Slot Filling Workflows | Pages 63–64 | `dependency_assistant` |
| **[`streaming_capability`](file:///c:/Users/VISHAL/office/joule_ai/streaming_capability/README.md)** | **SSE Streamed Messages** (`type: streamed-message`) & Token Streaming | Pages 70–72 | `streaming_assistant` |
| **[`upload_capability`](file:///c:/Users/VISHAL/office/joule_ai/upload_capability/README.md)** | **User Confirmation Dialogs** (`type: user-confirmation`) & File Upload Processing Workflows | Pages 73–74 | `upload_assistant` |

---

## ⚡ Quick Deployment Guide

To deploy and test any capability, update **`da.sapdas.yaml`** to point to the desired capability folder, then run:

```powershell
cd C:\Users\VISHAL\office\joule_ai

# 1. Lint capability descriptor
joule lint ./<capability_folder>

# 2. Compile into runtime artifact (.daar)
joule compile ./<capability_folder>

# 3. Deploy digital assistant to BTP
joule deploy da.sapdas.yaml

# 4. Launch in browser
joule launch <assistant_name>
```
