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

    #### How Do They Work? The Two-Step Process

    Parameterized queries work through a two-step communication process between your Application (your code) and the Database Server. The template is not permanently stored in the database; it is sent by the application with each request.

    **Step 1: Prepare (Sending the Template) 📝**

    First, the application sends the SQL command template to the database server. This template contains placeholders where the data will go.

    * Application says: "Hey Database, get ready to execute this command: `SELECT * FROM users WHERE email = ?`."
    * Database does:
      1. Receives this template.
      2. Checks it for syntax errors.
      3. Creates an optimized execution plan for this specific query structure.
      4. Holds this plan in memory and replies, "Okay, I'm prepared and waiting for the data."

    Example Code (PHP):

    PHP

    ```
    // The SQL template with a placeholder
    $sql_template = "SELECT * FROM employees WHERE name = ?";

    // Sending the template to the database to be prepared
    $statement = $pdo->prepare($sql_template);
    ```

    **Step 2: Execute (Sending the Data) ✉️**

    Next, the application sends the user's input to the database in a separate transmission.

    * Application says: "For the template you just prepared, fill the first `?` with this value: `'user@example.com'`."
    * Database does:
      1. Receives `'user@example.com'`.
      2. Treats this value strictly as data. Even if the data contains malicious SQL code like `'; DROP TABLE users;--'`, it's just seen as a simple string of text.
      3. Safely inserts the data into the pre-compiled execution plan.
      4. Executes the complete, safe query.

    Example Code (PHP):

    PHP

    ```
    // The (potentially malicious) data from the user
    $userInput = "' OR 1=1; --";

    // Send this data separately to be executed with the prepared statement
    // The database will safely handle $userInput as a literal string
    $statement->execute([$userInput]);
    ```

    #### Why Is This Secure? The Core Principle

    The security of parameterized queries comes from one simple but powerful concept: separation of concerns.

    * The command is parsed first, without any user data. The database builds its understanding of what to do based only on the trusted template from the developer.
    * The data is supplied later and never parsed as a command. By the time the user data arrives, the database is already in "data-filling mode," not "command-interpreting mode."

    This makes it impossible for an attacker to "inject" malicious commands because their input will never be executed. The database will simply search for a user with a very strange name, like `"' OR 1=1; --"`, find nothing, and the attack is neutralized. ✅
