---
tags:
  - email
  - smtp
Date: 2024-05-07T23:43:00
---


That's how SMTP works. It's purely a protocol for dropping a mail off at a mail server, either by your originating client or an interim server dropping it off at another upstream server. SMTP servers work in chains; your client drops off at godaddy, today's might drop off at an upstream server, upstream server drops off at destination (or another upstream; many servers might handle it on the way).

If SMTP stored mails in a sent mail folder, every server involved in the delivery chain would have a copy of every mail it ever transited - hard disks would be full in minutes!

Storing in a Sent Items folder is typically a function of a different service like IMAP. After a heavyweight mail client like Outlook sends a mail using SMTP it stores a copy of what was sent using an IMAP connection (same mail server, probably- totally different protocol). If you want the same functionality you have to build an IMAP client into your program too

If this isn't easy to understand, a real world analogy:

You open Word, write a letter, print it, post it (=SMTP), and turn your computer off. The document is not in My Documents folder (=sent items folder). If you want it there they you have to click Save in Word, save into your My Documents folder (=IMAP storage in sent items folders