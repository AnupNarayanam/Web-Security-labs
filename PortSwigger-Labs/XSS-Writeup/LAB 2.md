# LAB 2 :

This lab asks us to identify and exploit a **`Stored XSS` vulnerability** in an application that stores user input without any encoding.

**Recap [ Stored XSS ] :** 
Happens when malicious input is saved by the server and later executed in other users’ browsers.

**Example :** in a database, comment field, or profile section).

**Cause :** Persistent storage of unsanitized user input that is later returned in the HTTP response without output encoding

**Solution :**

Solved this lab By just choosing any post and entering this script which triggers the Stored XSS .

```
<script>alert(1)</script>
```

![L2-1](Images/L2-1.png)

![L2-2](Images/L2-2.png)

But when i go back to the Blog !!

![L2-3](Images/L2-3.png)

Now this below image explains that every user who visit this post will see the above alert triggerd box and it will exec in their systems as well !

![L2-4](Images/L2-4.png)

---

---
