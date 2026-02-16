# Lab 1: Reflected XSS into HTML Context (No Encoding)

### 🚩 Vulnerability Overview
This lab demonstrates how the search functionality can be exploited via Reflected XSS to execute arbitrary JavaScript using the `alert()` function.

### 📝 Recap [ Reflected XSS ]
Reflected XSS occurs when user input is immediately returned in the server’s response without proper validation or encoding.

### 🔗 Example
It executes only when a victim clicks a specially crafted link containing the payload.

### 🔍 Cause
The application takes user input from the search parameter and directly includes it in the HTML response without sanitizing or encoding it.

### 🛠️ Solution
Solved this by executing the following script in the search area:

```
<script>alert("Noob")</script>
```
<img src="Images/L1-1.png" width="600" alt="Img 1 ">
<br><br>
<img src="Images/L1-2.png" width="600" alt="Img 2 ">
