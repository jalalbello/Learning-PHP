## Form handling

```html
Action welcome PHP will redirect the data to welcome.php page
<form action="welcome.php" method="post">
```

Both GET and POST create an array 

keys are the names of the form controls and values are the input data from the user.

$_GET is an array of variables passed to the current script via the URL parameters.

$_POST is an array of variables passed to the current script via the HTTP POST method.

Use **GET** to send non sensitive data, here is an example of the url we get when using get, and entering "aa" in the **name** and "aa" in the **email**

```html
http://localhost/First%20Program/welcome.php?name=aa&email=aa
<!--* The limitation is about 2000 characters -->
```

Information sent from a form with the POST method is invisible to others (all names/values are embedded within the body of the HTTP request) and has no limits on the amount of information to send.

it is not possible to bookmark the page.


```html
<form method="post" action="php echo htmlspecialchars($_SERVER["PHP_SELF"]);?>">
```

the $_SERVER["PHP_SELF"] sends the submitted form data to the page itself, instead of jumping to a different page. This way, the user will get error messages on the same page as the form.