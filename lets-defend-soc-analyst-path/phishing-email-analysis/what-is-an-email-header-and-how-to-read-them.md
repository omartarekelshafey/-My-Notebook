# What is an Email Header and How to Read Them?

**What does the Email Header do?**

Allows you to identify the sender and recipient&#x20;

Thanks to the "From" and "To" fields in the header, you can find out who is sending an email and who is receiving it. If we look at the email above, which you have downloaded in "eml" format, we can see that it was sent from "ogunal@letsdefend.io" to "info@letsdefend.io".

Spam Blocker

It is possible to detect spam emails using header analysis and various other methods. This prevents people from receiving SPAM emails.

Tracking an Email’s Route

You can use the **email header** to see the path the email took.\
Even if it says it came from "[ogunal@letsdefend.io](mailto:ogunal@letsdefend.io)", it might be **a fake server using that name**.\
The header helps you check if the email really came from the **real letsdefend.io domain** or not.



#### Important Fields

**From**: The 'From' field in an Internet header shows the name and email address of the sender.\
\
**To**: this field in the mail header contains the details of the recipient of the email, including their name and email address. Such as CC (carbon copy) and BCC (blind carbon copy) also fall under this category, as they all contain details of your recipients.\
\
\
**Date**: This is the timestamp showing when the email was sent.\
\
**Subject**: The subject is the topic of the email. It summarizes the content of the entire message body.\
\
**Return-Path** : The return path header is used to identify where bounce messages should be sent if email delivery fails

**Reply-To** is the email address where replies will be sent, which can be different from the sender’s (From) address.

\
**Domain Key and DKIM Signatures**: Domain Key and Domain Key Identified Mail (DKIM) are email signatures that help email service providers identify and authenticate your emails, similar to SPF signatures.\
\
**Message-ID:** The Message-ID header is a unique combination of letters and numbers that identifies each email. No two emails will have the same Message ID.

**MIME-Version:** MIME-Version indicates that the email supports Multipurpose Internet Mail Extensions (MIME), a standard that allows emails to include different content types such as images, videos, attachments, and HTML. MIME converts non-text content into encoded text formats (like Base64) so they can be transmitted over SMTP, which only supports plain text.

\
**Received:** The Received section lists each mail server that an email has passed through before arriving in the recipient's inbox. It's listed in reverse chronological order - the mail server at the top is the last server the email message passed through, and the mail server at the bottom is where the email originated.\
\
**X-Spam Status: The** X-Spam Status shows you the spam score of an email message.\
First, it'll highlight if a message is classified as spam.\
It then shows the spam score of the email and the spam threshold for the email.\
An email can either meet or exceed an inbox's spam threshold. If it's too spammy and exceeds the threshold, it's automatically classified as spam and sent to the Spam folder.
