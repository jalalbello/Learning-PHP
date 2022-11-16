## Date and Time

```
date(format,timestamp)
```
format	Required. Specifies the format of the timestamp
timestamp	Optional. Specifies a timestamp. Default is the current date and time

|           |                                                                       |
| :-------- | --------------------------------------------------------------------: |
| format    |                       Required. Specifies the format of the timestamp |
| timestamp | Optional. Specifies a timestamp. Default is the current date and time |

Learn more here: https://www.w3schools.com/php/php_date.asp

## Add files with php

> require will produce a fatal error (E_COMPILE_ERROR) and stop the script
> 
> include will only produce a warning (E_WARNING) and the script will continue

## File handling php

Common errors are: 
- editing the wrong file, 
- filling a hard-drive with garbage data, 
- and deleting the content of a file by accident.

### **readfile() function reads a file and writes it to the output buffer.**

## A better way than readfile()

### **fopen()**

```php
Syntax:
fopen(filename, mode)
```

> **Modes**

|           |                                                                                                                                                              |
| :-------- | -----------------------------------------------------------------------------------------------------------------------------------------------------------: |
| r         |                                                                                  Open a file for read only. File pointer starts at the beginning of the file |
| w         |      Open a file for write only. Erases the contents of the file or creates a new file if it doesn't exist. File pointer starts at the beginning of the file |
| a         | Open a file for write only. The existing data in file is preserved. File pointer starts at the end of the file. Creates a new file if the file doesn't exist |
| x         |                                                                         Creates a new file for write only. Returns FALSE and an error if file already exists |
| r+        |                                                                                 Open a file for read/write. File pointer starts at the beginning of the file |
| w+        |      Open a file for read/write. Erases the contents of the file or creates a new file if it doesn't exist. File pointer starts at the beginning of the file |
| a+        | Open a file for read/write. The existing data in file is preserved. File pointer starts at the end of the file. Creates a new file if the file doesn't exist |
| x+        |                                                                         Creates a new file for read/write. Returns FALSE and an error if file already exists |

### **fread()**

```php
Syntax:
fread(filename, maximum of bytes to be read)
// Example
fread($myfile,filesize("webdictionary.txt"));
// File is read from start to end
```

### **fclose()**


> It's a good programming practice to close all files after you have finished with them. You don't want an open file running around on your server taking up resources!

### **Read Single Line - fgets()**

### **feof()** Checks if end of file has been reached

Its usefull for looping over data of unkown length

```php
while(!feof($myfile)) {
  echo fgets($myfile) . "<br>";
}
```

### **fgetc() function is used to read a single character from a file.**


## Create a file

With fopen() and mode **w** or **a**

```php
   $myfile = fopen("helloworld.txt", "w") or die("Unable to write file!");
```
> **Note**: If u can't create a file check **persmissons**

## PHP Write to File - fwrite()

## Write to a file

```php
fwrite($myfile, $txt);
fwrite($myfile, " ");
```

## Uploading a file

Make sure to do this in the **php.ini**

```php
// ; Whether to allow HTTP file uploads.
// ; https://php.net/file-uploads
file_uploads=On
```
Maksure sure to have methode **POST** and multipart/form-data **attribute**

> The Html
```html
<form action="upload.php" method="post" enctype="multipart/form-data">
  Select image to upload:
  <input type="file" name="fileToUpload" id="fileToUpload">
  <input type="submit" value="Upload Image" name="submit">
</form>
```

```php
PHP $_FILES
The global predefined variable $_FILES is an associative array containing items uploaded via HTTP POST method.
$_FILES['file']['name']
```

Checking if POST is set
```php
$var = '';
// This will evaluate to TRUE so the text will be printed.
if (isset($var)) {
    echo "This var is set so I will print.";
}
```
```php
$TARGET_DIR = "uploads/";
$TARGET_FILE = $TARGET_DIR  . basename($_FILES["fileToUpload"]["name"];//* Name is not an attr or id, its a key to the array )
$uploadOk = 1;
$imageFileType =strtolower(pathinfo($TARGET_FILE, PATHINFO_EXTENSION));

// **Check if Image is not** fake

if(isset($_POST["submit"])){
    $CHECK = getimagesize($_FILES["fileToUpload"]["tmp_name"]);
    if($CHECK ==! false){
        echo "file is an image" . $CHECK["mime"] . ".";
        // * MIME = Multipurpose Internet Mail Extensions
        $uploadOk = 1;
    } else {
        echo "File is not an image";
        $uploadOk = 0;
    }
}
```

>$target_dir = "uploads/" - specifies the directory where the file is going to be placed
>
>$target_file specifies the path of the file to be uploaded
>
>$uploadOk=1 is not used yet (will be used later)
>
>$imageFileType holds the file extension of the file (in lower case)
>
>Next, **check if the image file** is an actual image or a fake image

### **Check if file already exists**

```php
if (file_exists($TARGET_FILE)){
    echo "Sorry File already exists";
    $uploadOk = 0; 
}
```

### **Limit File Size**

```php
if ($_FILES["fileToUpload"]["size"] > 500 000){
    echo "Sorry file too large";
    $uploadOk = 0;  
}
```

### **Limit File Type**

```php
// * Alow certain file types
// If only all of these is false, it will throw the error 
if($imageFileType != "jpg" && $imageFileType != "png" && $imageFileType != "jpeg"
&& $imageFileType != "gif" ) {
  echo "Sorry, only JPG, JPEG, PNG & GIF files are allowed.";
  $uploadOk = 0;
}
```

### **Check if Upload sucessfull**

```php
// Check if $uploadOk is set to 0 by an error
if ($uploadOk == 0) {
  echo "Sorry, your file was not uploaded.";
// if everything is ok, try to upload file
} else {
  if (move_uploaded_file($_FILES["fileToUpload"]["tmp_name"], $target_file)) {
    echo "The file ". htmlspecialchars( basename( $_FILES["fileToUpload"]["name"])). " has been uploaded.";
  } else {
    // * This happened due to an error in my XAMP, that has nothing to do with the script, so I was able to know we passed all checks but file was not uploaded
    echo "Sorry, there was an error uploading your file.";
  }
}
```

### **File security**

> Make sure to clean filenames when printing them, they could have a script as the file name

### **Php Cookies**

> set the cookie with httpOnly, which is recommended, since it helps to diminish the negative consequences of an XSS attack.
> 
A cookie is a small file, that the server puts on the clt computer, each time the clt requests a page, it will send the cookie too, we can both create and retrieve cookies

Create Cookie:

```php
setcookie(name, value, expire, path, domain, secure, httponly);
// * Only the name parametere is required
```

Modify cookie:

Set it again with setcookie()

Delete cookie:

Do a setcookie() function with an expiration date in the past:

```php
// Delete cookie
setcookie("user", "", time() - 3600);
```

Check if cookies are enabled:

```php
// First set it
setcookie("test_cookie", "test", time() + 3600, '/');
```

```php
// Second check it 
if(count($_COOKIE) > 0) {
  echo "Cookies are enabled.";
} else {
  echo "Cookies are disabled.";
}
```
> You might need to put them in **two diffrent** php tags

### **Php Sessions**

A web server (HTTP address) does not maintain **STATE**, and therefore cannot know **who we are**, and **what we do**

A session is a way to store info in vars to be used across multiple pages

Its not stored on the users computer

They last until the users **closes** the browser
- How does it work? How does it know it's me?:

sessions set a user-key on the user's computer,  when a session is opened on another page, it scans the computer for a user-key. If there is a match, it accesses that session, if not, it starts a new session.

- Start a Session :

```php
// Start the session
session_start();
```

- Set a Session:

```php
// with the PHP global variable: $_SESSION
$_SESSION["favanimal"] = "cat";
```

 - Print Contents of a session:


**print_r**:
It is a built-in function in print_r in PHP that is used to print or display the contents of a variable. It essentially prints human-readable data about a variable.

```php
print_r($_SESSION);
```

- Modify Content of a session

```php
// overwriting the session variable
$_SESSION["favcolor"] = "yellow";
```

- Destory a php session

> use **both** session_unset() and session_destroy()
```php
// remove all session variables
session_unset();

// destroy the session
session_destroy();
```


### **PHP Filters**
Php filters are used to **Validate**(if its in proper form) or **Sanitize**(if it has illegal char) data

> Filters List 
<table>
<tr><td>int</td><td>257</td></tr><tr><td>boolean</td><td>258</td></tr><tr><td>float</td><td>259</td></tr><tr><td>validate_regexp</td><td>272</td></tr><tr><td>validate_domain</td><td>277</td></tr><tr><td>validate_url</td><td>273</td></tr><tr><td>validate_email</td><td>274</td></tr><tr><td>validate_ip</td><td>275</td></tr><tr><td>validate_mac</td><td>276</td></tr><tr><td>string</td><td>513</td></tr><tr><td>stripped</td><td>513</td></tr><tr><td>encoded</td><td>514</td></tr><tr><td>special_chars</td><td>515</td></tr><tr><td>full_special_chars</td><td>522</td></tr><tr><td>unsafe_raw</td><td>516</td></tr><tr><td>email</td><td>517</td></tr><tr><td>url</td><td>518</td></tr><tr><td>number_int</td><td>519</td></tr><tr><td>number_float</td><td>520</td></tr><tr><td>add_slashes</td><td>523</td></tr><tr><td>callback</td><td>1024</td></tr>
</table>

### Php filter_var() Function

It can **both** validate and sanitize data

```php
Syntax:
filter_var(var, FILTER_SANITIZE_STRING))
// Can take other types of filters aswell
```

Validate int:

```php
if (filter_var($int, FILTER_VALIDATE_INT) === 0 || !filter_var($int, FILTER_VALIDATE_INT) === false) {
  echo("Integer is valid");
} else {
  echo("Integer is not valid");
}
// filter_var($int, FILTER_VALIDATE_INT) === 0  is used cuz if $int was set to 0, the function without it will exec else statement
```

Validate IP adress :

```php
// Results in a **boolean**
filter_var($ip, FILTER_VALIDATE_IP)
```
Validate and Sanitize URL :

```php
$url = filter_var($url, FILTER_SANITIZE_URL);
// Validate url
if (!filter_var($url, FILTER_VALIDATE_URL) === false) 
```
> For more filters : https://www.w3schools.com/php/php_ref_filter.asp

Validate an Integer Within a Range:

```php
if (filter_var($int, FILTER_VALIDATE_INT, array("options" => array("min_range"=>$min, "max_range"=>$max))
// the function accepts an options array, which again (depending on which options you're going to use) accepts one or more sub arrays
```

Validate IPV6 adress :

```php
$ip = "2001:0db8:85a3:08d3:1319:8a2e:0370:7334";

if (!filter_var($ip, FILTER_VALIDATE_IP, FILTER_FLAG_IPV6) === false)

```
Validate URL - Must Contain QueryString :

A query string is a part of a uniform resource locator (URL) that assigns values to specified parameters.

```php
if (!filter_var($url, FILTER_VALIDATE_URL, FILTER_FLAG_QUERY_REQUIRED) === false)
```

**Validate STRING FLAGS:**

FILTER_FLAG_STRIP_LOW
```php
Remove characters with ASCII value < 32
```
FILTER_FLAG_STRIP_HIGH
```php
Remove characters with ASCII value > 127
filter_var($str, FILTER_SANITIZE_STRING, FILTER_FLAG_STRIP_HIGH)
```

### **PHP Anon Functions**

```php
$var = function ($x) {return pow($x,3);};
// Function above has no name, making it anon
```
### **PHP Call back Functions with Anon functions**

A Callback if a function that has another function as its argument

> Example of a callback function
```php
function my_callback($item) {
  return strlen($item);
}
```
> Example of a callback function using an **anon** function as its **arg**
```php
$lengths = array_map( function($item) { return strlen($item); } , $strings);
```

> Practical example of a call back function

```php
function exclaim($str) {
  return $str . "! ";
}

function ask($str) {
  return $str . "? ";
}

function printFormatted($str, $format) {
  // Calling the $format callback function
  echo $format($str);
}

// Pass "exclaim" and "ask" as callback functions to printFormatted()
printFormatted("Hello world", "exclaim");
// function exclaim(Hello world)
printFormatted("Hello world", "ask");
// function ask(Hello world)
```

