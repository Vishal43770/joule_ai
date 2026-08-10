# UI Message Variations & Response Context Capability (`sample_capability`)

This capability demonstrates **Function to Scenario to GenAI Response Generation** and all **7 UI Message Variations** in SAP Joule, based on pages 41–44 and 165–180 of the *Joule Development Guide*.

---

## 📁 File Structure

```text
sample_capability/
├── capability.sapdas.yaml          # Capability metadata descriptor
├── README.md                       # Documentation
├── functions/
│   └── fetch_weather_info.yaml     # Dialog function implementing status update, set-variables, and 7 UI message variations
└── scenarios/
    └── fetch_weather.yaml          # Scenario mapping slots, target function, and response_context attributes
```

---

## 💡 Key Architectural Concepts

### 1. All 7 UI Message Variations (`type: message`)

1. **`text`**: Standard Markdown text output.
2. **`card`**: Structured visual feature card with status badges (`success`, `warning`, `error`).
3. **`list`**: Vertical list layout of items.
4. **`carousel`**: Horizontal scrollable swipe cards.
5. **`ui5integrationCard`**: SAP Fiori Integration Dashboard Card driven by YAML manifest object.
6. **`illustrated_message`**: SAP Fiori SVG illustration (`tntSuccess`).
7. **`likert_scale`**: Interactive rating prompt (1–5 scale) for user feedback.

---

### 2. Interactive Feedback Capture (`likert_scale` Slot Filling)

Likert scale ratings act as interactive slot fillers. When a user taps a rating button (e.g. `5`), Joule triggers Action Group 2 (`condition: 'weather_rating != null'`) to record and confirm the rating score!

---

## 🛠 Joule CLI Commands

Run these commands inside `C:\Users\VISHAL\office\joule_ai`:

```powershell
# 1. Lint the capability
joule lint ./sample_capability

# 2. Compile the capability
joule compile ./sample_capability

# 3. Deploy the digital assistant
joule deploy da.sapdas.yaml

# 4. Launch the assistant
joule launch weather_assistant
```
