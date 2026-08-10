# File Upload & User Confirmation Capability (`upload_capability`)

This dedicated capability demonstrates **User Confirmation Dialogs (`type: user-confirmation`)**, **File Processing Workflows**, and **Chat `+` Attachment Button comparisons**, based on pages 73–74 of the *Joule Development Guide*.

---

## 📁 File Structure

```text
upload_capability/
├── capability.sapdas.yaml          # Capability metadata descriptor (v3.28.0)
├── README.md                       # Documentation
├── functions/
│   └── process_upload.yaml         # Dialog function executing user confirmation & file processing
└── scenarios/
    └── process_upload.yaml         # Scenario linking document upload intent
```

---

## 💡 Key Architectural Concepts

### 1. User Confirmation Dialogs (`type: user-confirmation`)

Used to prompt the user with interactive approval buttons (`[ Yes, Upload ]` / `[ No, Cancel ]`) before executing sensitive enterprise operations:

```yaml
- type: user-confirmation
  scripting_type: "spel"
  content:
    title: "Confirm Document Upload"
    subtitle: "Would you like to process and upload your document file?"
    button_labels:
      confirm: "Yes, Upload"
      cancel: "No, Cancel"
  confirmation_variable: upload_confirmed
```

---

### 2. Capability Confirmation vs. Global Chat `+` Attachment Button

| Feature | Built-in Chat `+` Button | Capability Confirmation / Upload |
|---|---|---|
| **Purpose** | Ask general Q&A about uploaded documents | Execute controlled enterprise workflows (e.g. S/4HANA PO approvals) |
| **Setup Required** | None (Built into Joule UI out of the box) | Configured via `user-confirmation` or `file-upload` in function YAML |
| **User Experience** | Click `+`, upload PDF, ask questions | Interactive confirmation bar with custom `Yes` / `No` buttons |

---

## 🛠 Joule CLI Commands

Run these commands inside `C:\Users\VISHAL\office\joule_ai`:

```powershell
# 1. Lint the capability
joule lint ./upload_capability

# 2. Compile the capability
joule compile ./upload_capability

# 3. Deploy the digital assistant
joule deploy da.sapdas.yaml

# 4. Launch the assistant
joule launch upload_assistant
```
