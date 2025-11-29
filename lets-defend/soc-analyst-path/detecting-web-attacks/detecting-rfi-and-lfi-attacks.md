# Detecting RFI & LFI Attacks

## what Is LFI & RFI

* **Local File Inclusion (LFI):** A vulnerability where a web application includes files from its **own server** based on user input without proper validation. Attackers can exploit this to read sensitive files, like password files, on the server.
* **Remote File Inclusion (RFI):** A vulnerability where a web application includes files from **external servers** based on user input without proper validation. Attackers can trick the server into executing malicious code hosted remotely.

## **How does LFI & RFI work?**

LFI and RFI occur when a web application includes files based on user input without validating it. If the application directly uses data provided by a user to build a file path, an attacker can manipulate that input to load unexpected files.

With **LFI**, the attacker uses directory traversal (e.g., `../`) to move up the folder structure and include sensitive local files from the server itself, such as `/etc/passwd`.

With **RFI**, the attacker provides a URL to a remote file, causing the server to load and execute malicious code hosted elsewhere.

In both cases, the problem happens because user input is trusted and not sanitized, allowing attackers to control which file gets included.

## **How to Prevent LFI & RFI?**

The most effective way to prevent RFI and LFI attacks is to make sure that all data received from a user is sanitized before it is used. Remember that client-based controls are easily bypassed. Therefore, you should always implement your controls on both the client and server sides.

## **Detecting LFI & RFI Attacks**

How can we detect and prevent LFI and RFI attacks?

* **When examining a web request from a user, examine all fields.**
* **Look for any special characters:** Within the data received from users, look for notations such as '/', \`.\`, \`\\\`.
* **Become familiar with files commonly used in LFI attacks:** In an LFI attack, the attacker reads the files on the server. Knowing the critical file names on the server will help you detect LFI attacks.
* **Look for acronyms such as HTTP and HTTPS:** In RFI attacks, the attacker injects the file into their own device and allows the file to run.
* To host a file, attackers usually set up a small web server on their own device and display the file using an HTTP protocol. You should therefore look for notations such as 'http' and 'https' to help you detect RFI attacks.

<br>
