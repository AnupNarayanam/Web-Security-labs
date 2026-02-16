# Lab 3: DOM XSS in Search Query Using document.write()

### 🚩 Vulnerability Overview  
This lab demonstrates a **DOM-based XSS** vulnerability in the search functionality, where user-controlled data from the URL is written directly into the page using `document.write()`.

---

### 📝 What is `location.search` ?

`location.search` returns the query string portion of a URL, including the `?`.

Example:
```
https://example.com/page?name=anup&age=21
```

```
console.log(location.search);
```

```
?name=anup&age=21
```

If a website takes `location.search` and directly writes it into the page using:

```
document.write(location.search);
```

An attacker could inject:

```
https://example.com/page?<script>alert(1)</script>
```


The browser would interpret and execute the script → Causing XSS.

---

### 📝 Recap [ DOM XSS ]

DOM XSS occurs when a vulnerability exists in client-side JavaScript, where user-controlled data (such as `location.search`, `location.hash`, or `document.URL`) is inserted into the page without proper sanitization.

---

### 🔍 Cause

The application reads user-controlled data from the URL and inserts it into the webpage using `document.write()` without validating or escaping it, allowing attackers to inject malicious scripts.

---

### 🛠️ Solution

While inspecting the page, it was observed that the search string was being inserted into an `img src` attribute.

<br>
<img src="Images/L3-1.png" width="600" alt="Img 1">
<br>

<br>
<img src="Images/L3-2.png" width="600" alt="Img 2">
<br>

From the inspect tab, it was confirmed that our search input is placed inside an `img src` attribute:

<br>
<img src="Images/L3-3.png" width="600" alt="Img 3">
<br>

The lab was solved using the following payload:

```
"><script>alert(1)</script>
```

Alternative payload:

```
"><svg onload=alert(1)>
```


---

### Why is the alternative payload better?

Sometimes:

- `<script>` tags are filtered or blocked.
- Certain contexts do not allow `<script>` execution.
- Event handlers like `onload` or `onerror` can bypass weak filtering mechanisms.

Therefore, the payload is often considered a more flexible bypass-style payload in real-world scenarios.





