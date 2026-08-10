# Custom Greeting Capability (`greeting_capability`)

This capability demonstrates **Static Parameter Injection** in scenario targets and **User Context Access** (`$transient.user`) inside SAP Joule dialog functions, based on page 47 of the *Joule Development Guide*.

---

## 📁 File Structure

```text
greeting_capability/
├── capability.sapdas.yaml          # Capability metadata descriptor
├── README.md                       # This documentation file
├── functions/
│   └── greet.yaml                  # Dialog function processing static parameters & user fallback
└── scenarios/
    └── greeting.yaml               # Scenario passing static target parameters & mapping response_context
```

---

## 💡 Code & Architecture Explained

### 1. Static Parameter Injection in Scenario (`scenarios/greeting.yaml`)

When a user utters a greeting prompt (*"Hello"* or *"Hi there"*), Joule matches the query to `greeting.yaml`. The scenario passes static parameters directly to the target dialog function `greet`:

```yaml
description: This functionality can be used to answer greetings.

target:
  type: function
  name: greet
  parameters:
    - name: client_name
      value: "Alex"                # Static parameter passed to function
    - name: greeting_message
      value: "Welcome to SAP Joule"# Static parameter passed to function

response_context:
  - value: greeting                # Must match key in function result block!
    description: Custom greeting details
```

---

### 2. Dialog Function Processing (`functions/greet.yaml`)

The dialog function receives `client_name` and `greeting_message` as input parameters. It uses SpEL scripting to set default fallbacks using `$transient.user.first_name` if needed:

```yaml
parameters:
  - name: client_name
    optional: true
  - name: greeting_message
    optional: true

action_groups:
  - actions:
      - type: set-variables
        variables:
          - name: name_val
            value: "<? client_name ?: ($transient.user.first_name ?: 'Valued User') ?>"
          - name: msg_val
            value: "<? greeting_message ?: 'Welcome to SAP Joule AI!' ?>"

      - type: message
        message:
          type: card
          content:
            title: "<? msg_val ?>, <? name_val ?>!"
            subtitle: "Custom Greetings Assistant"
            description:
              value: "Hello **<? name_val ?>**! How can I assist you with your tasks today?"
              markdown: true
            status: "Connected"
            statusState: "success"

result:
  greeting: "<? msg_val ?> <? name_val ?>"
```

---

## 🛠 Joule CLI Commands

Run these commands inside `C:\Users\VISHAL\office\joule_ai`:

```powershell
# 1. Lint the capability
joule lint ./greeting_capability

# 2. Compile the capability
joule compile ./greeting_capability

# 3. Deploy the digital assistant
joule deploy da.sapdas.yaml

# 4. Launch the assistant
joule launch greeting_assistant
```
