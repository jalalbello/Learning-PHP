The $_SERVER["PHP_SELF"] variable can be used by hackers!

If PHP_SELF is used in your page then a user can enter a slash (/) and then some Cross Site Scripting (XSS) commands to execute.

```html
Safe syntax
<form method="post" action="php echo htmlspecialchars($_SERVER["PHP_SELF"]);?>">
```

### Validate an http form

1. pass all variables through PHP's htmlspecialchars() function
2. Strip unnecessary characters (extra space, tab, newline) from the user input data (with the PHP trim() function)
3. Remove backslashes (\) from the user input data (with the PHP stripslashes() function)
4. create a function that will do all the checking for us (which is much more convenient than writing the same code over and over again).

```php
function test_input($data) {
  $data = trim($data);
  $data = stripslashes($data);
  $data = htmlspecialchars($data);
  return $data;
}
```