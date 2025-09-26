# Detecting SQL Injection Attacks

### SQL Injection (SQLi)

* **Definition**: An attack where unsanitized user input is injected directly into **SQL queries** → lets attackers manipulate the database.
* **Why it still exists**:
  * Developers using raw SQL.
  * Frameworks with built-in SQLi issues.
  * Bad implementation / misuse of frameworks.

***

### Types of SQL Injection

1. **In-band SQLi (Classic)**
   * Request + Response happen on the **same channel**.
   * Easiest for attackers to exploit.
2. **Inferential SQLi (Blind)**
   * Attacker doesn’t see direct output.
   * Relies on **observing server behavior** (true/false responses, time delays, etc.).
3. **Out-of-band SQLi**
   * Data exfiltrated via **another channel** (e.g., DNS, HTTP requests).
   * Used when in-band/ blind aren’t possible.

***

