A Php script can be placed anywhere in the doc

It ends with .php

> It normally contains HTML Tags and some php scripting code

Php elements end with a **;**

<br>

### Php Case sensitivity
<br>

**Keywords, functions, user defined function** are *not case sensitive* they are **case insensitive**

```php
<?php
ECHO "Hello World!<br>";
echo "Hello World!<br>";
EcHo "Hello World!<br>";
?>
```

> **_NOTE:_** all variable names are case-sensitive!

### **Variables**

it starts with a $ followed by the var name

### Template literals (Template strings)

> Following code will produce same output
```php
<?php
$txt = "W3Schools.com";
echo "I love " . $txt . "!";
?>
<?php
$txt = "W3Schools.com";
echo "I love $txt!";
?>
``` 

### **Loosely Typed Language**

Php associates the data type depending on its value

Since data types are not set in a strict sense, we can a int to a str

```php
$x = "5";
$y = 4;
echo $x + $y;
// outputs 9
```

> **_NOTE:_**  enabling the strict requirement, it will throw a "Fatal Error" on a type mismatch.

```php
Fatal error: strict_types declaration must be the very first statement in the script in C:\xampp\htdocs\First program\HelloWorld.php on line 11
```

### **PHP variables scope**

*Global and local*:

A variable delcared *outside* a function is **GLOBAL** and cannot be accessed **inside** a function

A var delacrted *inside* is **LOCAL** and cannot be accesed **outside** a function

### Global Keyword

This keyword can be used to access a global var within a function

Php stores all Global vars in an array called **$GLOBALS[index]**

We can use this array to acess the vars **without the keyword**

```php
function myTest() {
  $GLOBALS['a'] = $GLOBALS['b'] + $GLOBALS['c'];
}
```

*Static*:

Normally when a function is executed, all its vars are deleted, howerver sometimes we want a local var Not to be deleted, for a further job.

To do this we use the **static** Keyword

```php
function myTest() {
  static $x = 0;
  echo $x;
  $x++;
}
```

### **ECHO / PRINT**

They are the same, excpet **print returns 1**

> Echo can take multiple parameters
> 
> Print can take only one arg
> 
> Echo is a bit faster

```php
echo "This ", "string ", "was ", "made ", "with multiple parameters.";
```

