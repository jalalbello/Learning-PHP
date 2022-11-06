For a complete reference of all array functions: https://www.w3schools.com/php/php_ref_array.asp

## count(), get length of the server

## Associative Arrays, 

They use named keys, that we assign to them.

They function like associative arrays

```php
Syntax
array("Peter"=>"35", "Ben"=>"37", "Joe"=>"43");
echo $age['Peter'],
```

### Loop Through an Associative Array

```php
foreach($age as $x => $x_value) {
  echo "Key=" . $x . ", Value=" . $x_value;
  echo "<br>";
}
```

### Multidimensional Arrays
```php
    $cars = array (
        array("Volvo",22,18),
        array("BMW",15,13),
        array("Saab",5,2),
        array("Land Rover",17,15)
      );

    echo $cars;
    for ($i = 0; $i < 4; $i++){
        echo "<p><b>Row number $i</b></p>";
        echo "<ul>";
    for ($i1 = 0; $i1 < 3; $i1++){
    echo "<li>".$cars[$i][$i1]. "</li>";
    }
    echo "</ul>";
    }
```

# sort()

sorts the array, in accesending alphabetical/numerical order

# rsort()

sort in reverse

# asort()

Sort in accending value

# ksort()
 
ascending order, according to keys

# krsort()

reverse of **ksort**()

# arsort

ascending order, according to value


