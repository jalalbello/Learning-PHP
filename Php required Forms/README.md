```php

<!DOCTYPE HTML>  
<html>
<head>
<style>
.error {color: #FF0000;}
</style>
</head>
<body>  

<?php
// define variables and set to empty values
$nameErr = $emailErr = $genderErr = $websiteErr = $name = $email = $gender = $comment = $website = "";

if ($_SERVER["REQUEST_METHOD"] == "POST") {
  if (empty($_POST["name"])) {
    $nameErr = "Name is required";
  } else {
    $name = test_input($_POST["name"]);
  }
  
  if (empty($_POST["email"])) {
    $emailErr = "Email is required";
  } else {
    $email = test_input($_POST["email"]);
  }
    
  if (empty($_POST["website"])) {
    $website = "";
  } else {
    $website = test_input($_POST["website"]);
  }

  if (empty($_POST["comment"])) {
    $comment = "";
  } else {
    $comment = test_input($_POST["comment"]);
  }

  if (empty($_POST["gender"])) {
    $genderErr = "Gender is required";
  } else {
    $gender = test_input($_POST["gender"]);
  }
}

function test_input($data) {
  $data = trim($data);
  $data = stripslashes($data);
  $data = htmlspecialchars($data);
  return $data;
}
?>

<h2>PHP Form Validation Example</h2>
<p><span class="error">* required field</span></p>
<form method="post" action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]);?>">  
  Name: <input type="text" name="name">
  <span class="error">* <?php echo $nameErr;?></span>
<!-- echo $nameErr, since its empty it will not display anything, if we post and the else statement gets trigered it will say *required  --> 
  <br><br>
  E-mail: <input type="email" name="email">
  <span class="error">* <?php echo $emailErr;?></span>
  <br><br>
  Website: <input type="url" name="website">
  <span class="error"><?php echo $websiteErr;?></span>
  <br><br>
  Comment: <textarea name="comment" rows="5" cols="40"></textarea>
  <br><br>
  Gender:
  <input type="radio" name="gender" value="female">Female
  <input type="radio" name="gender" value="male">Male
  <input type="radio" name="gender" value="other">Other
  <span class="error">* <?php echo $genderErr;?></span>
  <br><br>
  <input type="submit" name="submit" value="Submit">  
</form>

<?php
echo "<h2>Your Input:</h2>";
echo $name;
echo "<br>";
echo $email;
echo "<br>";
echo $website;
echo "<br>";
echo $comment;
echo "<br>";
echo $gender;
?>

</body>
</html>
```

## Making sure the input fields are correct

### **Name Check**

We are going to use the following php code for **name** Validation

```php
$name = test_input($_POST["name"]);
if (!preg_match("/^[a-zA-Z-' ]*$/",$name)) {
  $nameErr = "Only letters and white space allowed";
}
```
> ---
```php
^[a-zA-Z-' ]*$
```
<p>^ <strong>Beginning.</strong> Matches the beginning of the string, or the beginning of a line if the multiline flag (m) is enabled.</p>
<p>[ <strong>Character set.</strong> Match any character in the set.</p>
<p>a-z <strong>Range.</strong> Matches a character in the range "a" to "z" (char code 97 to 122). Case sensitive.</p>
<p>A-Z <strong>Range.</strong> Matches a character in the range "A" to "Z" (char code 65 to 90). Case sensitive.</p>
<p>- <strong>Character.</strong> Matches a "-" character (char code 45).</p>
<p>' <strong>Character.</strong> Matches a "'" character (char code 39).</p>
<p><strong>Character.</strong> Matches a SPACE character (char code 32).</p>
<p>] &nbsp;</p>
<p>* <strong>Quantifier.</strong> Match 0 or more of the preceding token.</p>
<p>$ <strong>End.</strong> Matches the end of the string, or the end of a line if the multiline flag (m) is enabled.</p>

--- 

### **Email Check**

The easiest and safest way to check whether an email address is well-formed is to use PHP's filter_var() function.

In the code below, if the e-mail address is not well-formed, then store an error message:

```
Syntax:

filter_var(var, filtername, options)
```

```php
// Sanitize email
$email = filter_var($email, FILTER_SANITIZE_EMAIL);

// Validate e-mail
if (filter_var($email, FILTER_VALIDATE_EMAIL)) {
    echo("$email is a valid email address");
} else {
    echo("$email is not a valid email address");
}
```

### **URL Check**

> Regex 
![Alt text](Annotation%202022-11-08%20233545.png)

```php
// Check if the url is valid
if (!preg_match("/\b(?:(?:https?|ftp):\/\/|www\.)[-a-z0-9+&@#\/%?=~_|!:,.;]*[-a-z0-9+&@#\/%=~_|]/i",$website)) {
    $websiteErr = "Invalid URL";
}
```