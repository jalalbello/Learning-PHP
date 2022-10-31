### If we want to specify the expected data type, we need to use

> declare(strict_types=1);

```php
declare(strict_types=1); // strict requirement

function addNumbers(int $a, int $b) {
  return $a + $b;
}
echo addNumbers(5, "5 days");
```

### Specify the expcted data type for the **return** statement

> , add a colon ( : ) and the type right before the opening curly ( { )

```php
function addNumbers(float $a, float $b) : float {
```

### Passing arguments 

They are passed by value, a copy of the value is used in the function, and the **var cannot be changed**

## Passing arguments by refrence

the & operator :
This means changes to the argument will change also the var that was passed in 

```php
function add_five(&$value) {
  $value += 5;
}

$num = 2;
add_five($num);
echo $num;
```