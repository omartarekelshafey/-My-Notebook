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

### How Does SQL Injection Work?

* Modern web apps accept user data and use it to build and run SQL queries. Login pages are common targets for SQL injection (SQLi).
* Typical login query template:

```sql
SELECT * FROM users WHERE username = 'USERNAME' AND password = 'USER_PASSWORD'
```

This asks the database: “Return user rows whose username equals `USERNAME` **and** whose password equals `USER_PASSWORD`.” If a matching row exists the application authenticates the user; otherwise login fails.

* Example with normal credentials:

```sql
username = john
password = supersecretpassword
```

becomes:

```sql
SELECT * FROM users WHERE username = 'john' AND password = 'supersecretpassword'
```

This is valid; if a matching row exists, login succeeds.

* If a user supplies an extra apostrophe (`'`) the SQL string can break, producing a syntax error. Example: `john'` can create a malformed query and trigger an error message, which attackers can use to learn about the database.
* Example attacker payload:

```
' OR 1=1 -- -
```

If inserted into the username field and concatenated into the query without sanitization, the resulting SQL becomes:

```sql
SELECT * FROM users WHERE username = '' OR 1=1 -- - AND password = 'supersecretpassword'
```

* `-- -` starts a comment, so everything after it is ignored. Removing the commented tail yields:

```sql
SELECT * FROM users WHERE username = '' OR 1=1
```

* `OR 1=1` is always true, so the WHERE clause matches rows regardless of actual credentials. The database returns rows (often the first row), and if the application treats any returned row as successful authentication the attacker gains access.
* This is a typical SQL injection pattern. Beyond bypassing authentication, attackers can sometimes execute other SQL commands (e.g., `xp_cmdshell`) depending on the database and privileges.

***

## **What Attackers Gain from SQL Injection Attacks**

To understand why SQL injection attacks are so important, let's take a look at what an SQL injection attack can do.

* Authentication bypass
* Command execution
* Exfiltration of sensitive data
* Creating/Deleting/Updating database entries

## **How to Prevent SQL Injections**

* **Use a framework:** Of course, just using a framework is not enough to prevent a SQL injection attack. However, it is still very important to use the framework according to the documentation.
* **Keep your framework up to date:** Keep your web application secure by following security updates according to the framework you use.
* **Always sanitize data received from a user:** Never trust data received from a user. In addition, sanitize all data (such as headers, URLs, etc.), not just form data.
*   **Avoid the use of raw SQL queries:** You may be in the habit of writing raw SQL queries, but you should take advantage of the security provided by the framework.\


    #### What Are Parameterized Queries?

    A Parameterized Query is a secure method for querying a database that strictly separates the SQL command from the user-provided data. Instead of mixing user input directly into the SQL string, placeholders (like `?`) are used in the SQL template. The user data is then sent separately and is treated only as data, never as an executable command.

    This technique is the primary defense against SQL Injection attacks.

    Analogy: Think of it as filling out a pre-printed form instead of writing a request from scratch.

    * The Form (The Template): A secure, unchangeable structure with blank fields for your data. Example: `"Find employee with Name: [_______]"`
    * Your Data: The information you write into the blank fields. Example: `"Ali"`

    No matter what you write in the blank field, it can never change the structure of the form itself.

## **Detecting SQL Injection Attacks**

As SOC analysts, it's crucial to detect SQL Injection attacks to prevent significant damage to an organization. Detection involves identifying both manual attacks and those launched by automated tools.

### **General Detection Methods**

1. Check All User Input:
   * Attacks aren't limited to form fields. You must inspect all areas of an HTTP request that come from the user, including headers like the `User-Agent`.
2. Look for SQL Keywords:
   * Scan user-submitted data for common SQL commands such as `INSERT`, `SELECT`, and `WHERE`.
3. Identify Special Characters:
   * Be alert for special characters commonly used in SQL syntax and attacks, such as apostrophes (`'`), dashes (`-`), and parentheses (`()`), within user data.
4.  Recognize Common Payloads:

    * Familiarize yourself with frequently used SQL injection payloads. Attackers often use standard payloads to probe for vulnerabilities, making them easier to spot if you know what to look for.

    **common payloads:** [**https://github.com/payloadbox/sql-injection-payload-list**](https://github.com/payloadbox/sql-injection-payload-list)

### **Detecting Automated SQL Injection Tools**

Attackers use automated tools like `Sqlmap` to find vulnerabilities efficiently. You can detect these tools using the following methods:

1. Analyze the User-Agent:
   * Automated tools often include their name and version in the `User-Agent` header of the requests they send.
2. Monitor Request Frequency:
   * These tools send a very high volume of requests per second to test payloads quickly. A normal user might send one request per second, so a high request rate from a single source is a strong indicator of an automated tool.
3. Inspect Payload Content:
   * Some tools embed their names directly into the test payloads. For example: `sqlmap’ OR 1=1`.
4. Note Payload Complexity:
   * Based on experience, payloads generated by automated tools tend to be more complex and intricate than those crafted manually by an attacker.

