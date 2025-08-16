# ✅ Chore-O-Matic

**Chore-O-Matic** is a Home Assistant blueprint that automatically adds and removes tasks from a to-do list based on defined triggers.
It prevents duplicates (case-insensitive, with whitespace trimmed) and lets you choose whether a task should be marked as completed or deleted entirely.

---

## ✨ Features

* Add a task when a trigger fires.
* Prevents duplicate tasks (case-insensitive, trims leading/trailing whitespace).
* Supports optional **task description** — can include **Jinja templates** (e.g., `{{ now().strftime("%H:%M") }}`).
* Supports optional **due time** relative to the moment the task is added (e.g., 2 hours, 1 day).
* Flexible removal options:

  * ✅ *Complete* — mark task as done.
  * ❌ *Delete entirely* — remove it from the list.

---

## 🔧 Inputs

| Field                | Description                                                          |
| -------------------- | -------------------------------------------------------------------- |
| **To-do list**       | Select the to-do list entity where the task will be managed.         |
| **Add trigger**      | Trigger that will add the task to the list.                          |
| **Remove trigger**   | Trigger that will complete or remove the task.                       |
| **Task name**        | The name of the task. Duplicate prevention is based on this.         |
| **Task description** | (Optional) Task details. Supports Jinja templating.                  |
| **Task due in**      | (Optional) Duration until the task is due (e.g., 2h, 1d).            |
| **Removal mode**     | Choose *Complete* (mark task done) or *Delete entirely* (remove it). |

---

## 📋 Example

Add a task **“Take out trash”** every Monday at 19:00, and mark it complete when the front door is opened.

* **Add trigger:**
  `Time → Monday 19:00`
* **Remove trigger:**
  `State → Binary sensor (door) → from off to on`
* **Task name:**
  `Take out trash`
* **Removal mode:**
  `Complete`

---

## 📝 Tips

* You can create multiple automations for different chores using this blueprint.
* Use Jinja templates in the description to add dynamic values, e.g.:

  ```
  Task description: "Added at {{ now().strftime('%H:%M') }}"
  ```
* If a task already exists (case-insensitive), it won’t be added again until it’s removed/completed.
