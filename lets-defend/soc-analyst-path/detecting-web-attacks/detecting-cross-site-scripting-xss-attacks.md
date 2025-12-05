# Detecting Cross Site Scripting (XSS) Attacks

## What is Cross-Site Scripting (XSS)?

Simply put, an XSS attack occurs when an application includes untrusted data in a new web page without proper validation or sanitization. When another user (the victim) visits this page, their browser will execute the attacker's malicious script, trusting it as a legitimate part of the website.

Since the malicious script executes within the context of a trusted site, it can access sensitive data such as cookies, session tokens, or any other information the browser stores for that site.

***

## Types of XSS

XSS vulnerabilities are primarily categorized based on how the attack interacts with the server and the browser.

### 1. Reflected XSS

* Concept: The malicious script is part of a URL sent to the victim by the attacker. When the victim clicks the link, the script is sent to the server, which then "reflects" it back as part of the HTML response to the browser, where it is executed.

### 2. Stored XSS

* Concept: The attacker injects the malicious script and saves it permanently on the target application (e.g., in a comment, a forum post, or a user profile).

***

### In-Depth Focus: DOM-based XSS

This modern type of XSS attack occurs entirely within the browser's environment.

* Concept: The server sends a clean page, but the legitimate JavaScript on that page reads malicious data from a Source (like a URL fragment) and injects it into the page using a dangerous Sink, causing the malicious script to execute.

#### The Core Components

* The DOM (Document Object Model): The programming interface for the web page's structure in the browser's memory. It is the "scene of the crime" where the attack takes place.
* The Source: The input gateway that allows user-controlled data to enter the JavaScript code. Common sources include parts of the URL like `location.hash` and `location.search`.
* The Sink: The dangerous execution point. It is a JavaScript function or property that takes data and executes it. A sink is not a variable for storage; it is the action that triggers the vulnerability, such as `element.innerHTML`.

#### The Attack Journey (Internal Trip)

The code's journey in DOM-based XSS is an internal trip within the browser only. The server sends a clean page, and after it loads, the page's own legitimate JavaScript reads the malicious payload from the local URL and executes it. The server never sees the attack.

## How Attackers Take Advantage of XSS Attacks & Scope of Impact

Because XSS is a client-based attack method, it may seem less important than other attack methods, but XSS attacks and their impact should not be taken for granted.<sup>1</sup>

Attackers can do the following with an XSS attack:<sup>2</sup>

* Steal a user’s session informat<sup>3</sup>ion: This allows the attacker to hijack the user's session and take over their account completely.
* Capture credentials: The script can create fake login forms to steal the user's username and password.
* Etc.: Other impacts include keylogging, content manipulation (defacement), and phishing by redirecting the user to malicious websites.

## **How to Prevent a XSS Vulnerability**

* **Sanitize data coming from a user:** Never trust data that you receive from a user. If user data needs to be processed and stored, it should first be encoded with "HTML Encoding" using special characters, only then can it be stored.
* **Use a framework:** Most frameworks come with preventative measures against XSS attacks.
* **Use the framework correctly:** Almost all frameworks used to develop web applications come with a sanitation feature, but if this is not used properly, there is still a chance for XSS vulnerabilities to occur.
* **Keep your framework up-to-date:** Frameworks are developed by humans, so they too can contain XSS vulnerabilities. However, these types of vulnerabilities are usually patched with security updates. You should therefore make sure that you have completed the security updates for your framework on a regular basis.

## **Detecting XSS Attacks**

As we mentioned in the previous lesson, according to a study by Acunetix, 75% of cyber-attacks are conducted through web applications. As XSS is one of the most commonly tested vulnerabilities, you will encounter it throughout your career as a SOC analyst.

* **Look for keywords:** The easiest way to detect XSS attacks is to look for keywords such as "alert" and "script" that are commonly used in XSS payloads.
* **Learn about commonly used XSS payloads:** Attackers tend to use the same payloads to look for vulnerabilities before exploiting an XSS vulnerability. Therefore, familiarizing yourself with commonly used XSS payloads would make it easier for you to detect XSS vulnerabilities. You can examine some commonly used payloads [here](https://github.com/payloadbox/xss-payload-list).
* **Check for the use of special characters:** Check data coming from a user to see if any special characters commonly used in XSS payloads, such as greater than (>) or less than (<), are present.

<br>

