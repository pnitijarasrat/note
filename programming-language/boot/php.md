# PHP

## Conditional Rendering

```php
class="body-<?php echo 'class-name' ?>"

<div class="coffee-info">
    <?php if ($selectedCoffee === 'espresso'): ?>
    <div id="espresso-info">
        <h1>Espresso ☕</h1>
    <?php else: ?>
    <div id="drip-coffee-info">
        <h1>Drip Coffee ☕</h1>
    </div>
    <?php endif; ?>
</div>
```

## Variable

```php
$var_name = value

<? php
$string = "test" . "concat" // use . to cancat string;
echo $string;

$name = "tar";
$lang = "php";
echo "$name is learning $lang";

$num = 2;
echo (42) . "\n";
echo ('5' + '6') . "\n"; // return 11
echo round(3.2222, 1); // return 3.2

$num *= 2 // now num is change
?>
```

## Debugging

```php
<?php
var_dump($num);
?>
```

## If Else Condition

```php
<?php
if (true) {
  // code
} else if {
  // another code
} else {
  // another one
}

// can do this too
if (true) // code
?>
```

## Checking Value

```php
<?php

isset() // check if declare
empty() // check if empty, '0' is considered empty
unset() // use to unset the var ,so inset() will return false

?>
```

## Array

```php
<?php

$items = array("item1", "item2")

// check if in array
in_array(element, array) // true false
count(array) // return length
array_search(element, array) // return index of element in array


?>
```

## Foreach

```php
<?php

// continue use to continue the loop
// break use to exit loop
foreach ($arrays AS $array) {
  if (true) continue;
  else break;
}

// $books is associated array
foreach ($books AS $book => $author) {
  if (true) continue;
  else break;
}

array_keys($books) // return array of all key in $books


?>
```

## end
