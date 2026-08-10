# Capability Context & Parameter Passing (`context_capability`)

This project demonstrates **Capability Context Variables** and **Target Parameter Passing** based on pages 61–62 of the *Joule Development Guide*.

---

## 📁 File Structure

```text
context_capability/
├── capability.sapdas.yaml          # Capability metadata descriptor
├── capability_context.yaml         # Declares capability context variables
├── README.md                       # Documentation
├── functions/
│   └── search_station.yaml         # Dialog function executing station search
└── scenarios/
    └── search_station.yaml         # Scenario linking slots, $capability_context target parameters, and context updates
```

---

## 💡 Key Architectural Concepts

### 1. Capability Context Definition (`capability_context.yaml`)

Defines session variables accessible across functions and scenarios within this capability:

```yaml
variables:
  - name: from_station_id
  - name: station_id
  - name: station_capacity
  - name: last_executed_scenario
```

---

### 2. Passing Context Variables & Static Strings (`scenarios/search_station.yaml`)

Scenario targets pass variables using `$capability_context.variable_name` or static strings:

```yaml
target:
  type: function
  name: search_station
  parameters:
    - name: from_station_id
      value: $capability_context.from_station_id # Passed from Capability Context
    - name: to_station_id
      value: Wiesloch-Walldorf                    # Static string parameter
```

---

### 3. Updating Capability Context with Function Results (`capability_context:`)

After function execution, scenario results write back into capability context:

```yaml
capability_context:
  - name: station_id
    value: $target_result.id                      # Writes function result ID into context
  - name: station_capacity
    value: $target_result.capacity                # Writes capacity into context
  - name: last_executed_scenario
    value: search_trainstation                    # Writes static string into context
```

---

## 🛠 Joule CLI Commands

Run these commands inside `C:\Users\VISHAL\office\joule_ai`:

```powershell
# 1. Lint the capability
joule lint ./context_capability

# 2. Compile the capability
joule compile ./context_capability

# 3. Deploy the assistant
joule deploy da.sapdas.yaml

# 4. Launch the assistant
joule launch context_assistant
```
