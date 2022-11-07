## They are vars that are built in and always accesible no matter the scope

<p>The PHP superglobal variables are:</p>
<ul>
  <li>$GLOBALS</li>
  <li>$_SERVER</li>
  <li>$_REQUEST</li>
  <li>$_POST</li>
  <li>$_GET</li>
  <li>$_FILES</li>
  <li>$_ENV</li>
  <li>$_COOKIE</li>
  <li>$_SESSION</li>
</ul>

## $GLOBALS

Php stores all global variables in an array called $GLOBALS[*index*].

How to use global vars insinde a function:

> Using standard syntax does not work, you need this syntax

```php
function addition() {
  $GLOBALS['z'] = $GLOBALS['x'] + $GLOBALS['y'];
}
```

## $_SERVER

Its a super global variable which holds information about headers, paths, and script locations.

```php
echo $_SERVER['HTTP_USER_AGENT'];
```

The following table lists the most important elements that can go inside $_SERVER:

## $_REQUEST

PHP $_REQUEST is a PHP super global variable which is used to collect data after submitting an HTML form.

## $_POST
Its widely used to pass a variable

```php
//* This code runs like in a loop, when u press submit button ther if gets executed
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // collect value of input field
    $name = htmlspecialchars($_REQUEST['fname']);
    // htmlspecialchars to protect my page from Cross Site Scripting (XSS) attack
    if (empty($name)) {
        echo "Name is empty";
    } else {
        echo $name;
    }
}
```

## $_GET

PHP $_GET is a PHP super global variable which is used to collect form data after submitting an HTML form with method="get".