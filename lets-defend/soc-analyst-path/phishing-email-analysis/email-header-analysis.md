---
description: >-
  Here are the key questions we need to answer when checking headings during a
  Phishing analysis:
---

# Email Header Analysis

* Was the email sent from the correct SMTP server?
* Are the data "From" and "Return-Path / Reply-To" the same?

## Was the email sent from the correct SMTP server?

To determine whether the email was sent from the correct server, we check the **Received** field, which shows the path the message took.\
In this case, the email came from the server **101\[.]99.94.116**.

<div align="left"><figure><img src="../../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure></div>

\
However, the sender appears to be from the domain **letsdefend.io**.

<div align="left"><figure><img src="../../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure></div>

\
Normally, the domain **letsdefend.io** should be using this server to send mail. To verify, we query the domain’s **MX servers** using a tool like **mxtoolbox.com**.\
The results showed that the domain **letsdefend.io** actually uses Google mail servers, with no relation to **101\[.]99.94.116** or **emkei\[.]cz**.

\
This analysis confirmed that the email was not sent from the legitimate address but was instead **spoofed**.

<div align="left"><figure><img src="../../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure></div>



## Are the data "From" and "Return-Path / Reply-To" the same?

To check if the **From** and **Return-Path / Reply-To** details are the same:

* Normally, the sender and the recipient of replies should be the same, except in exceptional cases.
* In **phishing attacks**, attackers may abuse this: for example, sending an email from Gmail/Hotmail with a name similar to a Google employee, claiming there is an invoice to pay. They then insert the real Google employee’s email address into the **Reply-To** field, so that if the victim replies, it looks like the reply is going to a legitimate email rather than the fake one.
* Therefore, all we need to do is compare the email addresses in the **From** and **Reply-To** sections.
* If they are different, the reply will go to another address (e.g., Gmail).

<div align="left"><figure><img src="../../../.gitbook/assets/image (30).png" alt="" width="335"><figcaption></figcaption></figure></div>

* However, a mismatch does not always mean the email is phishing. We must look at the entire event: Is there a malicious attachment? A suspicious URL? Or misleading content?
* If the mismatch is combined with malicious content, we can confirm it is a **phishing email**.
* In the next lesson, the data in the body of the email will be analyzed.



