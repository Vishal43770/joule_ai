# Scenario Dependencies & Slot Sources (`dependency_capability`)

This capability demonstrates **Scenario Dependencies (`sources:`)** and **Slot Auto-Filling** based on pages 63–64 of the *Joule Development Guide*.

---

## 📁 File Structure

```text
dependency_capability/
├── capability.sapdas.yaml              # Capability descriptor
├── README.md                           # Documentation
├── functions/
│   └── purchase/
│       ├── get_pr.yaml                 # Returns Purchase Requisition ID (PR-88402)
│       └── create_po.yaml              # Creates PO using pr_id slot
└── scenarios/
    └── purchase/
        ├── get_pr.yaml                 # Target scenario producing $target_result.id
        └── create_po.yaml              # Consuming scenario declaring sources dependency
```

---

## 💡 Key Architectural Concepts

### 1. Declaring Scenario Dependencies (`sources:`)

In `scenarios/purchase/create_po.yaml`, the `pr_id` slot declares a dependency source on `purchase/get_pr`:

```yaml
slots:
  - name: pr_id
    description: ID of the purchase requisition the new purchase order is based on.
    sources:
      - type: scenario
        name: purchase/get_pr           # Source scenario to execute if slot is missing
        key: $target_result.id          # Extracts result ID from source scenario
```

### 2. How Joule Executes the Workflow Automatically:

1. **User Request**: *"Create a purchase order"*
2. **Slot Check**: Joule sees that `create_po` requires slot `pr_id`.
3. **Dependency Auto-Resolution**: Instead of asking the user to manually type a PR ID, Joule looks at `sources:`, executes `purchase/get_pr`, extracts `PR-88402`, and auto-fills `pr_id`!
4. **Execution**: Joule passes `pr_id = PR-88402` to `purchase/create_po` and creates the Purchase Order (`PO-90021`) seamlessly!

---

## 🛠 Joule CLI Commands

Run these commands inside `C:\Users\VISHAL\office\joule_ai`:

```powershell
# 1. Lint the capability
joule lint ./dependency_capability

# 2. Compile the capability
joule compile ./dependency_capability

# 3. Deploy the assistant
joule deploy da.sapdas.yaml

# 4. Launch the assistant
joule launch dependency_assistant
```
