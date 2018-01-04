# String Interpolator

[![Build Status](https://travis-ci.org/Visual-Craft/string-interpolator.svg?branch=master)](https://travis-ci.org/Visual-Craft/string-interpolator)

PHP library which provides string interpolation (variable expansion) functionality

## Install
```sh
composer require visual-craft/string-interpolator
```

## Usage

#### Instantiate interpolator object
```php
use VisualCraft\StringInterpolator\StringInterpolator;

$interpolator = new StringInterpolator();
```

#### String interpolation
```php
$result = $interpolator->interpolate('Demonstration $var1 $var2.', [
    'var1' => 'of',
    'var2' => 'interpolation',
]);
// $result === "Demonstration of interpolation."
```

Variable name can be enclosed with '{' and '}' to separate from the rest of the string:
```php
$result = $interpolator->interpolate('test${var1}test', [
    'var1' => '123',
]);
// $result === "test123test"
```

'$var_name' can be escaped with '\\':
```php
$result = $interpolator->interpolate('$var1 \$var2', [
    'var1' => '123',
]);
// $result === "123 $var2"
```

`VisualCraft\StringInterpolator\MissingVariableException` will be thrown if variable is missing:
```php
$result = $interpolator->interpolate('$var1 $var2', [
    'var1' => '123',
]);
// PHP Fatal error:  Uncaught VisualCraft\StringInterpolator\MissingVariableException: Missing variable 'var2'
```

#### Get variables names from subject
```php
$result = $interpolator->getVariablesNames('Demonstration $var1 $var2.');
// $result === ['var1', 'var2']
```

#### Get variables counts from subject
```php
$result = $interpolator->getVariablesCounts('Demonstration $var1 $var2. $var1');
// $result === ['var1' => 2, 'var2' => 1]
```

## Tests
```sh
composer install --dev
vendor/bin/kahlan
```

## License
MIT
