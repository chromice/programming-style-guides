# PHP coding style guide

**Version:** 1.1.0
**Date**: March 19, 2014

This guide is based on [PSR-0], [PSR-1], [PSR-2] coding style guides, with some bits borrowed from Wordpress [PHP][Wordpress PHP] and [HTML][Wordpress HTML] coding standards.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119].

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[PSR-1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[PSR-2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
[Wordpress PHP]: http://make.wordpress.org/core/handbook/coding-standards/php/
[Wordpress HTML]: http://make.wordpress.org/core/handbook/coding-standards/html/


## 1. Overview

- The rules outlined in this document MUST be _consistently_ followed. They MAY be _consistently_ broken, but only for a very good reason, which MUST be discussed before the project commences.

- Files MUST use only `<?php ?>` and `<?= ?>` tags.

- Files MUST use only UTF-8 without BOM and the Unix LF (linefeed) line ending.

- Files SHOULD *either* declare symbols (classes, functions, constants, etc.) *or* cause side-effects (e.g. generate output, change .ini settings, etc.) but SHOULD NOT do both.

- Namespace and class names MUST be declared in `StudlyCaps`.

- Class properties and constants MUST be declared in lower case with underscore separators.

- Method and function names MUST be declared in lower case with underscore separators.

- Code MUST use tabs for indenting, not spaces.

- There MUST NOT be a hard limit on line length; the soft limit MUST be 120 characters; lines SHOULD be 80 characters or less.

- There MUST be one blank line after the `namespace` declaration, and there MUST be one blank line after the block of `use` declarations.

- Opening braces for classes MUST go on the next line, and closing braces MUST go on the next line after the body.

- Opening braces for methods and functions MUST go on the next line, and closing braces MUST go on the next line after the body.

- Visibility MUST be declared on all properties and methods; `abstract` and `final` MUST be declared before the visibility; `static` MUST be declared after the visibility.
  
- Control structure keywords MUST have one space after them; method and function calls MUST NOT.

- Opening braces for control structures MUST go on the next line, and closing braces MUST go on the next line after the body.

- Opening parentheses for control structures MUST NOT have a space after them, and closing parentheses for control structures MUST NOT have a space before.

- Presentation and business logic MUST be separate.

- Alternative syntax MUST be used for control structures in HTML templates.

- Code MUST generally be well commented, simple and clean.

This following examples illustrate some of the rules below as a quick overview:


### 1.1. Declaration example

```php
<?php

namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

/*
    An implementation of FooInterface for BarClass.
*/
class Foo extends Bar implements FooInterface
{
    /*
        A sample method.
        
        Accepts two arguments:

        - $a can be any value
        - $b may be any value other than NULL.
    */
    public function sample_method($a, $b = null)
    {
        if ($a === $b)
        {
            bar();
        }
        elseif ($a > $b)
        {
            $foo->bar($arg_1);
        }
        else
        {
            BazClass::bar($arg_2, $arg_3);
        }
    }
    
    /*
        Bar class factory
    */
    final public static function bar()
    {
        // method body
    }
}
```

### 1.2. Declaration example

```php
<?php 

$title = Pages::current()->title();

$page_number = isset($_GET);
$per_page = 10;
$articles = Articles::find_all_by_page($page_number, $per_page);

?>
<h1><?= $title ?></h1>

<?php if (count($articles) < 1): ?>
    <p>No articles were found.</p>
<?php else: ?>
<?php   foreach ($articles as $article): ?>
    <article>
        <h2><?= $article->title() ?></h2>
        <?= $article->content() ?>
    </article>
<?php   endforeach ?>
<?php endif ?>
```


## 2. General

### 2.1. PHP tags

PHP code MUST use the long `<?php ?>` tags or the short-echo `<?= ?>` tags; it MUST NOT use the other tag variations.


### 2.2. Files

All PHP files MUST:

- Use only UTF-8 without BOM.
- Use the Unix LF (linefeed) line ending.
- End with a single blank line.

The closing `?>` tag MUST be omitted from files containing only 
PHP.

A file SHOULD *either* declare new symbols (classes, functions, constants, etc.) and cause no other side effects, *or* it SHOULD execute logic with side effects, but SHOULD NOT do both.

The phrase "side effects" means execution of logic not directly related to declaring classes, functions, constants, etc., *merely from including the file*.

"Side effects" include but are not limited to: generating output, explicit use of `require` or `include`, connecting to external services, modifying ini settings, emitting errors or exceptions, modifying global or static variables, reading from or writing to a file, and so on.

The following is an example of a file with both declarations and side effects; i.e, an example of what to avoid:

```php
<?php
// side effect: change ini settings
ini_set('error_reporting', E_ALL);

// side effect: loads a file
include "file.php";

// side effect: generates output
echo "<html>\n";

// declaration
function foo()
{
    // function body
}
```

The following example is of a file that contains declarations without side effects; i.e., an example of what to emulate:

```php
<?php
// declaration
function foo()
{
    // function body
}

// conditional declaration is *not* a side effect
if (!function_exists('bar'))
{
    function bar()
    {
        // function body
    }
}
```


### 2.3. Lines

There MUST NOT be a hard limit on line length.

The soft limit on line length MUST be 120 characters; automated style checkers MUST warn but MUST NOT error at the soft limit.

Lines SHOULD NOT be longer than 80 characters; lines longer than that SHOULD be split into multiple subsequent lines of no more than 80 characters each.

There MUST NOT be trailing whitespace at the end of non-blank lines.

No more than 2 blank lines MAY be added to improve readability and to indicate related blocks of code.

There MUST NOT be more than one statement per line.

Long lines MAY be split into more. Each additional line MAY be indented and MUST begin with a operator.

```php
<?php
$foo = 'This is a very long string which would be split into two'
    . ' right about now. If it were much longer, like it is now'
    . ' it would be split again.';
```

Same logic would apply to long logical conditions:

```php
<?php
if (!isset($foo) && !isset($bar)
|| $foo === 'A very long value...'
&& $bar === 'Another long value...')
{
    # code...
}
```


### 2.4. Indenting and alignment

Code MUST use tabs for indenting, not spaces. The use of spaces to horizontally align related information on multiple lines is permitted, but SHOULD be used sparingly.

```php
<?php
$foo    = 'foo';
$bar    = 'bar';
$foobar = 'foobar';
```

The above example demonstrates a valid use of spaces for alignment, provided `$foo`, `$bar` and `$foobar` variables are indeed related.

For associative arrays, values SHOULD start on a new line and MUST be indented. 

```php
<?php
$my_array = array(
    'foo'     => 'some value',
    'foo_2'   => 'another value',
    'foo_3'   => 'one more value' ,
    'foo_3_4' => 'yet another value',
);
```

> Note the comma after the last array item: this is recommended because it makes it easier to change the order of the array, and makes for cleaner diffs when new items are added.


### 2.5. Keywords, constants and variables

[PHP keywords] MUST be in lower case

Compile-time constants `__CLASS__`, `__DIR__`, `__FILE__`, `__FUNCTION__`, etc MUST be in upper case. 

The PHP constants `true`, `false`, and `null` MUST be in lower case.

The PHP global variables `$_GET`, `$_POST`, `$_REQUEST`, `$_SERVER`, etc MUST be in upper case.

All user defined variables MUST be in lower case.

[PHP keywords]: http://php.net/manual/en/reserved.keywords.php


### 2.6. Strings

Both single and double quotes MAY be used in string declarations. Strings that do not use parameter evaluation MUST use single quotes.

```php
<?php
echo 'This a regular string';
echo "This string contains parameters: '${foo}' and '${bar}' ";
```

### 2.7. Regular Expressions

Perl compatible regular expressions ([PCRE], `preg_` functions) MUST be used in preference to their POSIX counterparts. The `/e` switch MUST NOT be used; `preg_replace_callback` MUST be used instead.

Single-quoted strings MUST be used for regular expressions since, contrary to double-quoted strings, they have only two metasequences: `\'` and `\\`.

[PCRE]: http://php.net/pcre

### 2.8. Comparison and checking

Strict comparison operators `===`, `!==` MUST be used to avoid side effects of type coercion.

`empty` function MUST be used for checking, if a variable contains an empty array, object, string.

`isset` function MUST only be used for checking is variable is declared and existence of an index.

## 3. Namespace and Use Declarations

When present, there MUST be one blank line after the `namespace` declaration.

When present, all `use` declarations MUST go after the `namespace` declaration.

There MUST be one `use` keyword per declaration.

There MUST be one blank line after the `use` block.

For example:

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ... additional PHP code ...

```


## 4. Classes, Properties, and Methods

The term "class" refers to all classes, interfaces, and traits.

### 4.1. Extends and Implements

The `extends` and `implements` keywords MUST be declared on the same line as the class name.

The opening brace for the class MUST go on its own line; the closing brace for the class MUST go on the next line after the body.

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // constants, properties, methods
}
```


### 4.2. Properties

Visibility MUST be declared on all properties.

The `var` keyword MUST NOT be used to declare a property.

There MUST NOT be more than one property declared per statement.

Property names SHOULD NOT be prefixed with a single underscore to indicate protected or private visibility.

A property declaration looks like the following.

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public $foo_bar = null;
}
```

### 4.3. Methods

Visibility MUST be declared on all methods.

Method names MAY be prefixed with a single underscore to indicate protected or private visibility.

Method names MUST NOT be declared with a space after the method name. The opening brace MUST go on its own line, and the closing brace MUST go on the next line following the body. There MUST NOT be a space after the opening parenthesis, and there MUST NOT be a space before the closing parenthesis.

A method declaration looks like the following. Note the placement of parentheses, commas, spaces, and braces:

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function foo_bar_baz($arg_1, &$arg_2, $arg_3 = [])
    {
        // method body
    }
}
```    

### 4.4. Method Arguments

In the argument list, there MUST NOT be a space before each comma, and there MUST be one space after each comma.

Method arguments with default values MUST go at the end of the argument list.

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function foo($arg_1, &$arg_2, $arg_3 = [])
    {
        // method body
    }
}
```


### 4.5. `abstract`, `final`, and `static`

When present, the `abstract` and `final` declarations MUST precede the visibility declaration.

When present, the `static` declaration MUST come after the visibility declaration.

```php
<?php
namespace Vendor\Package;

abstract class ClassName
{
    protected static $foo;

    final public static function bar()
    {
        // method body
    }

    abstract protected function zim();
}
```


### 4.6. Method and Function Calls

When making a method or function call, there MUST NOT be a space between the method or function name and the opening parenthesis, there MUST NOT be a space after the opening parenthesis, and there MUST NOT be a space before the closing parenthesis. In the argument list, there MUST NOT be a space before each comma, and there MUST be one space after each comma.

```php
<?php
bar();
$foo->bar($arg_1);
Foo::bar($arg_2, $arg_3);
```

Argument lists MAY be split across multiple lines, where each subsequent line is indented once. When doing so, the first item in the list MUST be on the new line, and there SHOULD be only one argument per line.

```php
<?php
$foo->bar(
    $long_argument,
    $longer_argument,
    $much_longer_argument
);
```

## 5. Control Structures

The general style rules for control structures are as follows:

- There MUST be one space after the control structure keyword
- There MUST NOT be a space after the opening parenthesis
- There MUST NOT be a space before the closing parenthesis
- The opening brace MUST go on the next line
- The structure body MUST be indented once
- The closing brace MUST be on the next line after the body

> The body of each structure MUST be enclosed by braces. This standardises how the structures look, and reduces the likelihood of introducing errors as new lines get added to the body.


### 5.1. `if`, `elseif`, `else`

An `if` structure looks like the following. Note the placement of parentheses, spaces, and braces; and that `else` and `elseif` are on the same line as the closing brace from the earlier body.

```php
<?php
if ($foo)
{
    // if body
}
elseif ($bar)
{
    // elseif body
}
else
{
    // else body;
}
```

The keyword `elseif` SHOULD be used instead of `else if` so that all control keywords look like single words.


### 5.2. `switch`, `case`

A `switch` structure looks like the following. Note the placement of parentheses, spaces, and braces. The `case` statement MUST be indented once from `switch`, and the `break` keyword (or other terminating keyword) MUST be indented at the same level as the `case` body. There MUST be a comment such as
`// no break` when fall-through is intentional in a non-empty `case` body.

```php
<?php
switch ($foo)
{
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```


### 5.3. `while`, `do while`

A `while` statement looks like the following. Note the placement of parentheses, spaces, and braces.

```php
<?php
while ($foo)
{
    // structure body
}
```

In contrast, a `do while` statement looks like the following. Note the placement of parentheses, spaces, and braces.

```php
<?php
do
{
    // structure body;
}
while ($foo);
```

### 5.4. `for`

A `for` statement looks like the following. Note the placement of parentheses, spaces, and braces.

```php
<?php
for ($i = 0; $i < 10; $i++)
{
    // for body
}
```

### 5.5. `foreach`
    
A `foreach` statement looks like the following. Note the placement of parentheses, spaces, and braces.

```php
<?php
foreach ($iterable as $key => $value)
{
    // foreach body
}
```

### 5.6. `try`, `catch`

A `try catch` block looks like the following. Note the placement of parentheses, spaces, and braces.

```php
<?php
try
{
    // try body
}
catch (FirstExceptionType $e)
{
    // catch body
}
catch (OtherExceptionType $e)
{
    // catch body
}
```

## 6. Closures

Closures MUST be declared with a space after the `function` keyword, and a space before and after the `use` keyword.

The opening brace MUST go on the same line, and the closing brace MUST go on the next line following the body.

There MUST NOT be a space after the opening parenthesis of the argument list or variable list, and there MUST NOT be a space before the closing parenthesis of the argument list or variable list.

In the argument list and variable list, there MUST NOT be a space before each comma, and there MUST be one space after each comma.

Closure arguments with default values MUST go at the end of the argument list.

A closure declaration looks like the following. Note the placement of parentheses, commas, spaces, and braces:

```php
<?php
$closure_with_args = function ($arg_1, $arg_2) {
    // body
};

$closure_with_args_and_vars = function ($arg_1, $arg_2) use ($var_1, $var_2) {
    // body
};
```

Note that the formatting rules also apply when the closure is used directly in a function or method call as an argument.

```php
<?php
$foo->bar($arg_1, function ($arg_2) use ($var_1) {
        // body
    }, $arg_3);
```

## 7. Mixing HTML and PHP code

Control structures MUST use alternative syntax (e.g. `if … endif`, `foreach … endforeach`, etc) when being used inside HTML templates.

When mixing PHP and HTML together, PHP blocks MUST be indented to match the surrounding HTML code. Closing PHP blocks MUST match the same indentation level as the opening block.

```php
<main id="main">
<?php if (empty($article)): ?>
    <article class="post">
        <h1>Not Found</h1>
        <div class="entry-content">
            <p>Apologies, but no results were found.</p>
            <?php include 'search_form.php'; ?>
        </div>
    </article>
<?php endif; ?>
</main>
```

All variable processing and calculations SHOULD be done at the top the file, and only the results SHOULD be mixed within HTML code.

## 8. Comments

The code MUST be generally well commented. 

Classes MUST have at least a one line description of the functionality they encompass. 

Methods and functions MUST have a one line description of what they do. Method and function description SHOULD state what result is returned, what exceptions may be thrown, etc.

Temporary or incomplete solutions MUST be commented as such using `FIXME` and `TODO` comments:

```php
// TODO: Add try/catch to prevent exception from bubbling up
// FIXME: foo() sometimes fails silently
foo($bar);
```

## 9. Best practices

[KISS], [DRY] and remember that you are writing code for the next person, who is going to debug it, so code clarity MUST be the priority.

[KISS]: http://en.wikipedia.org/wiki/KISS_principle
[DRY]: http://en.wikipedia.org/wiki/Don%27t_repeat_yourself

### 9.1. Use descriptive names

Names MUST be concise, descriptive, humanistic and consistent with the naming conventions of the whole project.

Variable and argument names MUST be nouns and SHOULD describe what data they contain. Names of variables containing an array MUST be plural.

```php
<?php
$page_title = 'Lorem ipsum dolor sit amet';
$dropdown_options = array('foo', 'bar', 'baz');
```

Function and method names MUST generally contain a verb and MUST describe _either_ how they affect the state _or_ what they return.

```php
<?php
interface CartInterface
{
    public function add_item($item);
    public function get_item($index);
    public function remove_item($index);
    public function clear();
}
```

### 9.2. Sanitise user input and escape output

User input MUST never be trusted. Form data MUST be validated. URI components MUST be validated and sanitised.

Content MUST be *either* escaped *or* sanitised when output in HTML context to prevent [cross site scripting][XSS].

Query parameters and data values MUST be escaped to prevent SQL injections.

[XSS]: http://en.wikipedia.org/wiki/Cross-site_scripting

### 9.3. Transfer and keep as little state as possible

Large arrays and hashes SHOULD NOT be passed to functions and methods.

Resources SHOULD be open 

### 9.2. Don’t repeat yourself

Copying and pasting chunks of code with slight modifications MUST be avoided. If code is being reused more then once, it MUST be encapsulated into a separate module.

### 9.3. Don’t mix business logic and presentation

Markup generation MUST NOT be done within functions or methods.

Business logic (SQL queries, input validation, data processing) MUST NOT be done within HTML/PHP templates.

### 9.4. Don’t leave garbage behind

Debug statements, purposeless code or unused classes, functions and methods MUST NOT be committed to the main branch.


