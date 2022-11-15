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

Modify cookie