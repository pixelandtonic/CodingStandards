PHP Coding Standards
====================

These standards are based on [PSR-1] and [PSR-2], save for a few religious
differences.

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”,
“SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be
interpreted as described in [RFC 2119].

[PSR-1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[PSR-2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[BOM]: http://www.w3.org/International/questions/qa-byte-order-mark.en.php



1. Overview
-----------

- Files MUST use the long `<?php ?>` tags.

- Files MUST use only UTF-8 without [BOM] for PHP code.

- Files SHOULD *either* declare symbols (classes, functions, constants, etc.)
  *or* execute logic with side effects, but SHOULD NOT do both.

- Only one class per file.

- Class names MUST be declared in `StudlyCaps`.

- Class constants MUST be declared in all upper case with underscore separators,
  with the exception of “enum” classes, whose class constants MUST be declared
  in `StudlyCaps`.

- Method, variable, and property names MUST be declared in `camelCase`.

- Code *indentation* MUST use tabs, not spaces.

- Inner-line code *alignment* MUST use spaces, not tabs.

- There MUST NOT be a hard limit on line length; the soft limit MUST be 120
  characters; lines SHOULD be 80 characters or less.

- There MUST be one blank line after the `namespace` declaration, and there
  MUST be one blank line after the block of `use` declarations.

- Opening braces for classes MUST go on the next line, and closing braces MUST
  go on the next line after the body.

- Opening braces for methods MUST go on the next line, and closing braces MUST
  go on the next line after the body.

- Visibility MUST be declared on all properties and methods; `abstract` and
  `final` MUST be declared before the visibility; `static` MUST be declared
  after the visibility.

- Control structures MUST have a blank line before and after them *unless* they
  exist at the very beginning/ending of the body of another function or control
  structure.

- Control structure keywords MUST NOT use their [alternative syntaxes] (`elseif`,
  `endif`, etc.).

- Control structure keywords MUST have one space after them; method and
  function calls MUST NOT.

- Opening braces for control structures MUST go on the next line, and closing
  braces MUST go on the next line after the body.

- Opening parentheses for control structures MUST NOT have a space after them,
  and closing parentheses for control structures MUST NOT have a space before.

- Equal signs used to define default function argument values MUST have a space
  before and after them.

[alternative syntaxes]: http://php.net/manual/en/control-structures.alternative-syntax.php


### 1.1. Example

This example encompasses some of the rules below as a quick overview:

```php
<?php
namespace Craft;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
    public function sampleFunction($a, $b = null)
    {
        if ($a === $b)
        {
            bar();
        }
        else if ($a > $b)
        {
            $foo->bar($arg1);
        }
        else
        {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // method body
    }
}
```



2. General
----------

### 2.1 Character Encoding

PHP code MUST use only UTF-8 without [BOM].


### 2.2 Line Endings

All PHP files MUST use Unix LF (linefeed) line endings.

All PHP files MUST end with a single blank line.


### 2.3. PHP Tags

PHP code MUST use the long `<?php ?>` tags; it MUST NOT use the other tag
variations.

The closing `?>` tag MUST be omitted from files containing only PHP.


### 2.4. Side Effects

A file SHOULD declare new symbols (classes, functions, constants,
etc.) and cause no other side effects, or it SHOULD execute logic with side
effects, but SHOULD NOT do both.

The phrase “side effects” means execution of logic not directly related to
declaring classes, functions, constants, etc., *merely from including the
file*.

“Side effects” include but are not limited to: generating output, explicit
use of `require` or `include`, connecting to external services, modifying ini
settings, emitting errors or exceptions, modifying global or static variables,
reading from or writing to a file, and so on.

The following is an example of a file with both declarations and side effects;
i.e, an example of what to avoid:

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

The following example is of a file that contains declarations without side
effects; i.e., an example of what to emulate:

```php
<?php
// declaration
function foo()
{
    // function body
}

// conditional declaration is *not* a side effect
if (! function_exists('bar'))
{
    function bar()
    {
        // function body
    }
}
```


### 2.5. Lines

There MUST NOT be a hard limit on line length.

The soft limit on line length MUST be 120 characters; automated style checkers
MUST warn but MUST NOT error at the soft limit.

Lines SHOULD NOT be longer than 80 characters; lines longer than that SHOULD
be split into multiple subsequent lines of no more than 80 characters each.

There MUST NOT be trailing whitespace at the end of non-blank lines.

Blank lines MAY be added to improve readability and to indicate related
blocks of code.

There MUST NOT be more than one statement per line.


### 2.6. Indentation and Alignment

Tabs MUST be used for indentation, and spaces MUST NOT be used for indentation.

The body of each class, function, control structure, etc. MUST be indented one
level (one tab) greater than its parent (with the exception of the braces).

Spaces MUST be used for inner-line alignment, and tabs MUST NOT be used for
inner-line alignment.

The following example demonstrates when to use tabs vs. spaces:

```
<?php
namespace∙Craft;

class∙Foo
{
⇥   function∙sampleFunction()
⇥   {
⇥   ⇥   return∙array(
⇥   ⇥   ⇥   'value'∙∙∙∙∙∙∙∙∙∙=>∙212,
⇥   ⇥   ⇥   'someOtherValue'∙=>∙212,
⇥   ⇥   );
⇥   }
}
```

These indentation/alignment standards account for the fact that code editors
have configurable tab widths. If someone prefers indentation to have the width
of two spaces, they can do that without modifying the code or going against
someone else’s preferences. The use of spaces for inner-line alignment prevents
the lines from going out of alignment in the event that one person’s editor uses
a different tab width than another’s.


### 2.7. Keywords and `true`/`false`/`null`

All PHP [keywords] MUST be in lower case.

The PHP constants `true`, `false`, and `null` MUST be in lower case.

[keywords]: http://php.net/manual/en/reserved.keywords.php


### 2.8. Strings

Strings MUST use single quote delimiters (e.g. `'string'`, not `"string"`)
*unless* the string contains escaped special characters (e.g. `\n`) and/or the
string is outputting variables (e.g. `"hey {$name}"`).

Variable names within strings MUST be delimited with braces (e.g.
`"hey {$name}"`, not `"hey $name"`).

String concatenation using the dot operator MUST NOT have spaces on either side
of the dot (e.g. `'hey '.$name`, not `'hey ' . $name`).

Strings MAY be concatenated across multiple lines, where each subsequent line is
indented once. When doing so, the dot operators MUST be placed at the ends of
the lines, with a single space before it.

```php
<?php
$string = 'Hello, '.$name."\n" .
    "Not {$name}? <a href=\"{$logoutUrl}\">Logout</a>";
```


### 2.9. Comments

Each class, property, and method MUST have DocBlock-style comments.

**Classes and Interfaces**

Class and interface DocBlock comments MUST have the following format:

```php
<?php
/**
 * One or two line short description about the class.
 *
 * Much longer in-depth description of the class that goes into great details about its functionality that follows the
 * ever important 120 character hard limit.
 *
 * @author    Pixel & Tonic, Inc. <support@pixelandtonic.com>
 * @copyright Copyright (c) 2014, Pixel & Tonic, Inc.
 * @license   http://buildwithcraft.com/license Craft License Agreement
 * @link      http://buildwithcraft.com
 * @package   craft.app.etc.templating
 * @since     1.0
 */
```

`@author`, `@copyright`, `@license`, `@link`, `@package` and `@since` SHOULD all
be specified.

**Methods**

Method DocBlock comments MUST have the following format:

```php
<?php
/**
 * One or two line short description about the method.
 *
 * Much longer in-depth description of the class that goes into great details about its functionality that follows the
 * ever important 120 character hard limit.
 *
 * @param AssetFolderModel $newLocation  The assetFolderModel representing the new location for the folder mirror. If
 *                                       none is specified, bad things will happen.
 * @param string|null      $sourcePath   The path on disk to the source folder.
 * @param array            $changedData  Any data that changed during the mirroring operation.
 *
 * @deprecated Deprecated in 1.3. Use {@link AppBehavior::getBuild() craft()->getBuild()} instead. This is now old and
 *             busted. Other important deprecation information.
 * @throws Exception|HttpException
 * @return bool|null true if the method was successful, false if not. A null value will be returned if it's Tuesday.
 *                   However, on Thursdays and full-moons, it will always be true.
 */
 ```

All short descriptions, long descriptions, parameter descriptions, deprecation
descriptions and return descriptions MUST follow the 120 character hard limit.
When referring to to other methods, classes or properties in the same class,
or other classes, the `@link` tag SHOULD be used.

**Specifying types**

For a list of valid types, see http://www.phpdoc.org/docs/latest/guides/types.html.

When specifying types, `int` MUST be used instead of `integer` and `bool` MUST
be used instead of `boolean`.

When specifying an array of types, the `int[]` or `Object[]` syntax MUST be
used.

**@param tag**

There MUST be a blank line before and after the `@param` tag declarations.

If a method parameter specifies a default (i.e. `$string = null`) the type for
that `@param` MUST be specified like `string|null`.

If multiple `@param` tags are used, then they MUST aligned vertically on the type,
the parameter name and the description.

**@return tag**

There MUST be a `@return` tag that specifies the type that gets returned.

If a method does not explicitly return anything, `@return null` must be used.

The `@return` tag MUST always be the last tag to be listed.

If a method returns more than one type, they MUST be separated by a `|`.
i.e. `@return bool|null`.

The return MUST specify a description of what is being returned. If the
description spans multiple lines, it MUST be aligned on the beginning of the
description text.

**@throws tag**

If a method throws an exception, the `@throws` tag MUST be specified.

If a method throws more that one type of exception, they must be separated by a
`|`. i.e. `@throws Exception|HttpException`.

**@deprecated tag**

If a method has been deprecated, the `@deprecated` tag MUST be used specifying
the version the method was deprecated in and, if applicable, an alternative
method or process to use instead.

If the description spans multiple lines, it MUST be aligned on the beginning of
the description text.

**@abstract, @static, @implements and @access tags**

These tags are obsolete and MUST not be used.

**Properties**

Property DocBlock commends MUST have the following format:

```php
/**
 * Whether to allow the Limit setting.
 *
 * @var string|null $allowLimit = null
 */
```
The property description MUST be above the `@var` tag and there MUST be a blank
line between them.

**Heading Level 1 comments**

Act as a heading for one or more methods following it, SHOULD use this style:

```php
// Public Methods
// =============================================================================
```

**Heading Level 2 comments**

Act as a heading for a group of lines of logical code, SHOULD use this style:

```php
// Create the field layout
// -----------------------------------------------------------------------------
```

**Heading Level 3 comments**

Explain what’s going on in the following line(s), SHOULD use this style:

```php
// Does an entry exist yet?
```

Heading Level 1 and 2 comments MUST have at least one blank line before and
after them. They SHOULD stretch 80 characters out (minus 4 characters for each
indentation level).

Heading Level 3 comments MUST have at least one blank line before them, and they
SHOULD NOT have any blank lines after them.



3. Namespace and Use Declarations
---------------------------------

When present, there MUST be one blank line after the `namespace` declaration.

When present, all `use` declarations MUST go after the `namespace`
declaration.

There MUST be one `use` keyword per declaration.

There MUST be one blank line after the `use` block.

For example:

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ...
```



4. Classes, Constants, Properties, and Methods
----------------------------------------------

The term “class” refers to all classes, interfaces, and traits.


### 4.1 Class Files

Each class should get its own dedicated file, and the file should be named with
the class name + “.php”.


### 4.2 Class Names

Class names MUST be declared in `StudlyCaps`.


### 4.3. `extends` and `implements`

The `extends` and `implements` keywords MUST be declared on the same line as
the class name.

The opening brace for the class MUST go on its own line; the closing brace
for the class MUST go on the next line after the body.

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

Lists of `implements` MAY be split across multiple lines, where each
subsequent line is indented once. When doing so, the first item in the list
MUST be on the next line, and there MUST be only one interface per line.

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constants, properties, methods
}
```


### 4.4. Constants

Class constants MUST be declared in all upper case with underscore separators,
*unless* the class is an “enum” class, whose sole purpose is to define constants
to help cut down on the use of magic strings throughout your code, in which case
class constasts MUST be declared using `StudlyCaps`.

For example, Craft’s DateTime class would be considered a normal class, so it
declares constants in all upper case with underscore separators:

```php
<?php
namespace Craft;

class DateTime extends \DateTime
{
    const W3C_DATE = 'Y-m-d';
    const MYSQL_DATETIME = 'Y-m-d H:i:s';
    const UTC = 'UTC';
    const DATEFIELD_24HOUR = 'Y-m-d H:i';
    const DATEFIELD_12HOUR = 'Y-m-d h:i A';

    public static function __toString()
    // ...
}
```

Craft’s ElementType class, on the other hand, is an “enum” class, so it declares
constants using `StudlyCaps`:

```php
namespace Craft;

abstract class ElementType extends BaseEnum
{
  const Asset       = 'Asset';
  const Category    = 'Category';
  const Entry       = 'Entry';
  const GlobalSet   = 'GlobalSet';
  const MatrixBlock = 'MatrixBlock';
  const Tag         = 'Tag';
  const User        = 'User';
}
```


### 4.5. Properties

Visibility MUST be declared on all properties.

The `var` keyword MUST NOT be used to declare a property.

There MUST NOT be more than one property declared per statement.

Property names MUST be declared in `$camelCase`.

Protected names SHOULD NOT be prefixed with a single underscore.

Private names MUST be prefixed with a single underscore to indicate private
visibility.

A property declaration looks like the following.

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public $foo = null;
}
```


### 4.6. Methods

Visibility MUST be declared on all non-magic methods.

Visibility MAY be declared on magic methods (`__toString()`, etc.).

Protected method names SHOULD NOT be prefixed with a single underscore.

Private method names MUST be prefixed with a single underscore to indicate
private visibility.

Method names MUST be declared in `camelCase()`.

Method names MUST NOT be declared with a space after the method name. The
opening brace MUST go on its own line, and the closing brace MUST go on the
next line following the body. There MUST NOT be a space after the opening
parenthesis, and there MUST NOT be a space before the closing parenthesis.

A method declaration looks like the following. Note the placement of
parentheses, commas, spaces, and braces:

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```


### 4.7. Method Arguments

In the argument list, there MUST NOT be a space before each comma, and there
MUST be one space after each comma.

Method arguments with default values MUST go at the end of the argument
list.

Equal signs used to define default argument values MUST have a space before and
after them.

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function foo($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

Argument lists MAY be split across multiple lines, where each subsequent line
is indented once. When doing so, the first item in the list MUST be on the
next line, and there MUST be only one argument per line.

When the argument list is split across multiple lines, the closing parenthesis
and opening brace MUST be placed on their own lines.

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    )
    {
        // method body
    }
}
```


### 4.8. `abstract`, `final`, and `static`

When present, the `abstract` and `final` declarations MUST precede the
visibility declaration.

When present, the `static` declaration MUST come after the visibility
declaration.

```php
<?php
namespace Vendor\Package;

abstract class ClassName
{
    protected static $foo;

    abstract protected function zim();

    final public static function bar()
    {
        // method body
    }
}
```


### 4.9. Method and Function Calls

When making a method or function call, there MUST NOT be a space between the
method or function name and the opening parenthesis, there MUST NOT be a space
after the opening parenthesis, and there MUST NOT be a space before the
closing parenthesis. In the argument list, there MUST NOT be a space before
each comma, and there MUST be one space after each comma.

```php
<?php
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```

Argument lists MAY be split across multiple lines, where each subsequent line
is indented once. When doing so, the first item in the list MUST be on the
next line, and there MUST be only one argument per line.

```php
<?php
$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
```

5. Control Structures
---------------------

The general style rules for control structures are as follows:

- Control structures MUST NOT use [alternative syntaxes].
- There MUST be one blank line before and after each control structure, *unless*
  it exist at the very beginning/ending of the body of another function or
  control structure.
- There MUST be one space after the control structure keyword
- There MUST NOT be a space after the opening parenthesis
- There MUST NOT be a space before the closing parenthesis
- The opening brace MUST be on the next line after the control structure
  declaration
- The structure body MUST be indented once
- The closing brace MUST be on the next line after the body

The body of each structure MUST be enclosed by braces. This standardizes how
the structures look, reduces the likelihood of introducing errors as new lines
get added to the body, and makes the code easier to debug.


### 5.1 Alternative Syntaxes

Control structures MUST NOT use [alternative syntaxes], *unless* it is in the
context of a PHP-based view file, whose primary responsibility is to output
HTML, etc., in which case control structures MUST use those alternative
syntaxes.


### 5.2. `if`, `else if`, `else`

An `if` structure looks like the following. Note the placement of parentheses,
spaces, and braces; and that `else` and `else if` are on the next line after the
closing brace from the earlier body.

```php
<?php
if ($expr1)
{
    // if body
}
else if ($expr2)
{
    // else if body
}
else
{
    // else body
}
```

The keyword `else if` MUST be used instead of `elseif` so there’s no chance of
it getting misread as “el serif”, which is Spanish for “the serif”.


### 5.3. `switch`, `case`

The general style rules for `switch` structures are as follows:

- The opening brace MUST be on the next line after the `switch` statement.
- The closing brace MUST go on the next line after the `switch` body.
- `case` statements MUST be indented once from `switch`.
- Non-empty `case` and `default` bodies MAY be wrapped in braces, on their own
  lines at the same indentation level as the `case` or `default` statement.
- `case` and `default` bodies MUST be indented once from their `case` or
  `default` statement.
- `break` and other terminating keywords MUST be indented at the same level as
  the `case` or `default` body.
- There MUST be a comment such as `// no break` when a fall-through is
  intentional on a non-empty `case` body.
- `case` and `default` structures MAY be separated by one blank line.

For example:

```php
<?php
switch ($expr)
{
    case 0:
    {
        echo 'First case, with a break';
        break;
    }

    case 1:
    {
        echo 'Second case, which falls through';
        // no break
    }

    case 2:
    case 3:
    case 4:
    {
        echo 'Third case, return instead of break';
        return;
    }

    default:
    {
        echo 'Default case';
        break;
    }
}
```


### 5.4. `while`, `do while`

A `while` statement looks like the following. Note the placement of
parentheses, spaces, and braces.

```php
<?php
while ($expr)
{
    // structure body
}
```

Similarly, a `do while` statement looks like the following. Note the placement
of parentheses, spaces, and braces.

```php
<?php
do
{
    // structure body;
}
while ($expr);
```


### 5.5. `for`

A `for` statement looks like the following. Note the placement of parentheses,
spaces, and braces.

```php
<?php
for ($i = 0; $i < 10; $i++)
{
    // for body
}
```


### 5.6. `foreach`

A `foreach` statement looks like the following. Note the placement of
parentheses, spaces, and braces.

```php
<?php
foreach ($iterable as $key => $value)
{
    // foreach body
}
```


### 5.7. `try`, `catch`

A `try catch` block looks like the following. Note the placement of
parentheses, spaces, and braces.

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

6. Closures
-----------

Closures MUST NOT be declared with a space after the `function` keyword.

Closures MUST be declared with a space before and after the `use` keyword.

The opening brace MUST go on the next line, and the closing brace MUST go on
the next line following the body.

There MUST NOT be a space after the opening parenthesis of the argument list
or variable list, and there MUST NOT be a space before the closing parenthesis
of the argument list or variable list.

In the argument list and variable list, there MUST NOT be a space before each
comma, and there MUST be one space after each comma.

Closure arguments with default values MUST go at the end of the argument
list.

Equal signs used to define default argument values MUST have a space before and
after them.

A closure declaration looks like the following. Note the placement of
parentheses, commas, spaces, and braces:

```php
<?php
$closureWithArgs = function($arg1, $arg2 = null)
{
    // body
};

$closureWithArgsAndVars = function($arg1, $arg2) use ($var1, $var2)
{
    // body
};
```

Argument lists and variable lists MAY be split across multiple lines, where
each subsequent line is indented once. When doing so, the first item in the
list MUST be on the next line, and there MUST be only one argument or variable
per line.

When the ending list (whether or arguments or variables) is split across
multiple lines, the closing parenthesis and opening brace MUST each be placed
on their own lines.

The following are examples of closures with and without argument lists and
variable lists split across multiple lines.

```php
<?php
$longArgs_noVars = function(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
)
{
   // body
};

$noArgs_longVars = function() use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
)
{
   // body
};

$longArgs_longVars = function(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
)
{
   // body
};

$longArgs_shortVars = function(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1)
{
   // body
};

$shortArgs_longVars = function($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
)
{
   // body
};
```

Note that the formatting rules also apply when the closure is used directly
in a function or method call as an argument.

```php
<?php
$foo->bar(
    $arg1,
    function($arg2) use ($var1)
    {
        // body
    },
    $arg3
);
```
