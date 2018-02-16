# Python Style Guide

This is my Python Style Guide.

It is inspired by [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html).

## Table of Contents
  1. [Semicolumns](#semicolumns)
  1. [Line Length](#line-length)
  1. [Parentheses](#parentheses)
  1. [Indentation](#indentation)
  1. [Blank Lines](#blank-lines)
  1. [Whitespace](#whitespace)
  1. [Shebang Line](#shebang-line)
  1. [Comments](#comments)
  1. [Classes](#classes)
  1. [Strings](#strings)
  1. [Files and Sockets](#files-and-sockets)
  1. [TODO Comments](#todo-comments)
  1. [Imports Formatting](#import-formatting)
  1. [Statements](#statements)
  1. [Access Control](#access-control)
  1. [Naming](#naming)
  1. [Main](#main)

## Semicolumns

Do not terminate your lines with semi-colons and do not use semi-colons to put two commands on the same line.

## Line Length

Maximum line length is *80 characters*.

Exceptions:

* Long import statements.
* URLs in comments.

Do not use backslash line continuation.

Make use of [Python's implicit line joining inside parentheses, brackets and braces](https://docs.python.org/3/reference/lexical_analysis.html#implicit-line-joining). If necessary, you can add an extra pair of parentheses around an expression.

```python
Yes: foo_bar(self, width, height, color='black', design=None, x='foo',
             emphasis=None, highlight=0)

     if (width == 0 and height == 0 and
         color == 'red' and emphasis == 'strong'):
```

When a literal string won't fit on a single line, use parentheses for implicit line joining.

```python
x = ('This will build a very long long '
     'long long long long long long string')
```

Within comments, put long URLs on their own line if necessary.

```python
Yes:  # See details at
      # https://www.example.com/us/developer/documentation/api/content/v2.0/csv_file_name_extension_full_specification.html
```

```python
No:  # See details at
     # https://www.example.com/us/developer/documentation/api/content/\
     # v2.0/csv_file_name_extension_full_specification.html
```

Make note of the indentation of the elements in the line continuation examples above; see the [indentation](#indentation) section for explanation.

## Parentheses

Use parentheses sparingly.

Do not use them in return statements or conditional statements unless using parentheses for implied line continuation. (See above.) It is however fine to use parentheses around tuples.

```python
Yes: if foo:
         bar()
     while x:
         x = bar()
     if x and y:
         bar()
     if not x:
         bar()
     return foo
     for (x, y) in dict.items(): ...
```

```python
No:  if (x):
         bar()
     if not(x):
         bar()
     return (foo)
```

## Indentation

Indent your code blocks with *4 spaces*.

Never use tabs or mix tabs and spaces. In cases of implied line continuation, you should align wrapped elements either vertically, as per the examples in the [line length](#line-length) section; or using a hanging indent of 4 spaces, in which case there should be no argument on the first line.

```python
Yes:   # Aligned with opening delimiter
       foo = long_function_name(var_one, var_two,
                                var_three, var_four)

       # Aligned with opening delimiter in a dictionary
       foo = {
           long_dictionary_key: value1 +
                                value2,
           ...
       }

       # 4-space hanging indent; nothing on first line
       foo = long_function_name(
           var_one, var_two, var_three,
           var_four)

       # 4-space hanging indent in a dictionary
       foo = {
           long_dictionary_key:
               long_dictionary_value,
           ...
       }
```

```python
No:    # Stuff on first line forbidden
       foo = long_function_name(var_one, var_two,
           var_three, var_four)

       # 2-space hanging indent forbidden
       foo = long_function_name(
         var_one, var_two, var_three,
         var_four)

       # No hanging indent in a dictionary
       foo = {
           long_dictionary_key:
               long_dictionary_value,
               ...
       }
```

## Blank Lines

Two blank lines between top-level definitions, one blank line between method definitions.

Two blank lines between top-level definitions, be they function or class definitions. One blank line between method definitions and between the `class` line and the first method. Use single blank lines as you judge appropriate within functions or methods.

## Whitespace

Follow standard typographic rules for the use of spaces around punctuation.

No whitespace inside parentheses, brackets or braces.

```python
Yes: spam(ham[1], {eggs: 2}, [])
```

```python
No:  spam( ham[ 1 ], { eggs: 2 }, [ ] )
```

No whitespace before a comma, semicolon, or colon. Do use whitespace after a comma, semicolon, or colon except at the end of the line.

```python
Yes: if x == 4:
         print x, y
     x, y = y, x
```

```python
No:  if x == 4 :
         print x , y
     x , y = y , x
```

No whitespace before the open paren/bracket that starts an argument list, indexing or slicing.

```python
Yes: spam(1)
```

```python
No:  spam (1)
```

```python
Yes: dict['key'] = list[index]
```

```python
No:  dict ['key'] = list [index]
```

Surround binary operators with a single space on either side for assignment (`=`), comparisons (`==, <, >, !=, <>, <=, >=, in, not in, is, is not`), and Booleans (`and, or, not`). Use your better judgment for the insertion of spaces around arithmetic operators but always be consistent about whitespace on either side of a binary operator.

```python
Yes: x == 1
```

```python
No:  x<1
```

Don't use spaces around the '=' sign when used to indicate a keyword argument or a default parameter value.

```python
Yes: def complex(real, imag=0.0): return magic(r=real, i=imag)
```

```python
No:  def complex(real, imag = 0.0): return magic(r = real, i = imag)
```

Don't use spaces to vertically align tokens on consecutive lines, since it becomes a maintenance burden (applies to :, #, =, etc.):

```python
Yes:
  foo = 1000  # comment
  long_name = 2  # comment that should not be aligned

  dictionary = {
      'foo': 1,
      'long_name': 2,
  }
```

```python
No:
  foo       = 1000  # comment
  long_name = 2     # comment that should not be aligned

  dictionary = {
      'foo'      : 1,
      'long_name': 2,
  }
```

## Shebang Line

Most .py files do not need to start with a `#!` line. Start the main file of a program with `#!/usr/bin/env python` with an optional single digit 2 or 3 suffix.

This line is used by the kernel to find the Python interpreter, but is ignored by Python when importing modules. It is only necessary on a file that will be executed directly.

## Comments

Be sure to use the right style for module, function, method and in-line comments.

### Doc Strings

Python has a unique commenting style using doc strings. A doc string is a string that is the first statement in a package, module, class or function. These strings can be extracted automatically through the `__doc__` member of the object and are used by `pydoc`. (Try running `pydoc` on your module to see how it looks.) We always use the three double-quote `"""` format for doc strings (per [PEP 257](https://www.python.org/dev/peps/pep-0257/)). A doc string should be organized as a summary line (one physical line) terminated by a period, question mark, or exclamation point, followed by a blank line, followed by the rest of the doc string starting at the same cursor position as the first quote of the first line. There are more formatting guidelines for doc strings below.

### Modules

Every file should contain license boilerplate. Choose the appropriate boilerplate for the license used by the project (for example, Apache 2.0, BSD, LGPL, GPL)

### Functions and Methods

As used in this section "function" applies to methods, function, and generators.

A function must have a docstring, unless it meets all of the following criteria:

* not externally visible
* very short
* obvious

A docstring should give enough information to write a call to the function without reading the function's code. A docstring should describe the function's calling syntax and its semantics, not its implementation. For tricky code, comments alongside the code are more appropriate than using docstrings.

Certain aspects of a function should be documented in special sections, listed below. Each section begins with a heading line, which ends with a colon. Sections should be indented two spaces, except for the heading.

Args:
  List each parameter by name. A description should follow the name, and be separated by a colon and a space. If the description is       too long to fit on a single 80-character line, use a hanging indent of 2 or 4 spaces (be consistent with the rest of the file).

  The description should mention required type(s) and the meaning of the argument.

  If a function accepts \*foo (variable length argument lists) and/or \**bar (arbitrary keyword arguments), they should be listed as       \*foo and \**bar.

Returns: (or Yields: for generators)
  Describe the type and semantics of the return value. If the function only returns None, this section is not required.

Raises:
  List all exceptions that are relevant to the interface.

```python
def fetch_bigtable_rows(big_table, keys, other_silly_variable=None):
    """Fetches rows from a Bigtable.

    Retrieves rows pertaining to the given keys from the Table instance
    represented by big_table.  Silly things may happen if
    other_silly_variable is not None.

    Args:
        big_table: An open Bigtable Table instance.
        keys: A sequence of strings representing the key of each table row
            to fetch.
        other_silly_variable: Another optional variable, that has a much
            longer name than the other args, and which does nothing.

    Returns:
        A dict mapping keys to the corresponding table row data
        fetched. Each row is represented as a tuple of strings. For
        example:

        {'Serak': ('Rigel VII', 'Preparer'),
         'Zim': ('Irk', 'Invader'),
         'Lrrr': ('Omicron Persei 8', 'Emperor')}

        If a key from the keys argument is missing from the dictionary,
        then that row was not found in the table.

    Raises:
        IOError: An error occurred accessing the bigtable.Table object.
    """
    pass
```

### Classes

Classes should have a doc string below the class definition describing the class. If your class has public attributes, they should be documented here in an Attributes section and follow the same formatting as a function's Args section.

```python
class SampleClass(object):
    """Summary of class here.

    Longer class information....
    Longer class information....

    Attributes:
        likes_spam: A boolean indicating if we like SPAM or not.
        eggs: An integer count of the eggs we have laid.
    """

    def __init__(self, likes_spam=False):
        """Inits SampleClass with blah."""
        self.likes_spam = likes_spam
        self.eggs = 0

    def public_method(self):
        """Performs operation blah."""
```

### Block and Inline Comments

The final place to have comments is in tricky parts of the code. If you're going to have to explain it at the next [code review](https://en.wikipedia.org/wiki/Code_review), you should comment it now. Complicated operations get a few lines of comments before the operations commence. Non-obvious ones get comments at the end of the line.

```python
# We use a weighted dictionary search to find out where i is in
# the array.  We extrapolate position based on the largest num
# in the array and the array size and then do binary search to
# get the exact number.

if i & (i-1) == 0:        # true iff i is a power of 2
```

To improve legibility, these comments should be at least 2 spaces away from the code.

On the other hand, never describe the code. Assume the person reading the code knows Python (though not what you're trying to do) better than you do.

```python
# BAD COMMENT: Now go through the b array and make sure whenever i occurs
# the next element is i+1
```

## Classes

If a class inherits from no other base classes, explicitly inherit from `object`. This also applies to nested classes.

```python
Yes: class SampleClass(object):
         pass


     class OuterClass(object):

         class InnerClass(object):
             pass


     class ChildClass(ParentClass):
         """Explicitly inherits from another class already."""
```

```python
No: class SampleClass:
        pass


    class OuterClass:

        class InnerClass:
            pass
```

Inheriting from `object` is needed to make properties work properly, and it will protect your code from one particular potential incompatibility with Python 3000. It also defines special methods that implement the default semantics of objects including `__new__`, `__init__`, `__delattr__`, `__getattribute__`, `__setattr__`, `__hash__`, `__repr__`, and `__str__`.

## Strings

Use the `format` method or the `%` operator for formatting strings, even when the parameters are all strings. Use your best judgement to decide between `+` and `%` (or `format`) though.

```python
Yes: x = a + b
     x = '%s, %s!' % (imperative, expletive)
     x = '{}, {}!'.format(imperative, expletive)
     x = 'name: %s; score: %d' % (name, n)
     x = 'name: {}; score: {}'.format(name, n)
```

```python
No: x = '%s%s' % (a, b)  # use + in this case
    x = '{}{}'.format(a, b)  # use + in this case
    x = imperative + ', ' + expletive + '!'
    x = 'name: ' + name + '; score: ' + str(n)
```

Avoid using the `+` and `+=` operators to accumulate a string within a loop. Since strings are immutable, this creates unnecessary temporary objects and results in quadratic rather than linear running time. Instead, add each substring to a list and `''.join` the list after the loop terminates (or, write each substring to a `io.BytesIO` buffer).

```python
Yes: items = ['<table>']
     for last_name, first_name in employee_list:
         items.append('<tr><td>%s, %s</td></tr>' % (last_name, first_name))
     items.append('</table>')
     employee_table = ''.join(items)
```

```python
No: employee_table = '<table>'
    for last_name, first_name in employee_list:
        employee_table += '<tr><td>%s, %s</td></tr>' % (last_name, first_name)
    employee_table += '</table>'
```

Be consistent with your choice of string quote character within a file. Pick `'` or `"` and stick with it. It is okay to use the other quote character on a string to avoid the need to \ escape within the string. GPyLint enforces this.

```python
Yes:
  Python('Why are you hiding your eyes?')
  Gollum("I'm scared of lint errors.")
  Narrator('"Good!" thought a happy Python reviewer.')
```

```python
No:
  Python("Why are you hiding your eyes?")
  Gollum('The lint. It burns. It burns us.')
  Gollum("Always the great lint. Watching. Watching.")
```

Prefer `"""` for multi-line strings rather than `'''`. Projects may choose to use `'''` for all non-docstring multi-line strings if and only if they also use `'` for regular strings. Doc strings must use `"""` regardless. Note that it is often cleaner to use implicit line joining since multi-line strings do not flow with the indentation of the rest of the program:

```python
Yes:
  print ("This is much nicer.\n"
         "Do it this way.\n")
```

```python
No:
  print """This is pretty ugly.
Don't do this.
"""
```

## Files and Sockets

Explicitly close files and sockets when done with them.

Leaving files, sockets or other file-like objects open unnecessarily has many downsides, including:

* They may consume limited system resources, such as file descriptors. Code that deals with many such objects may exhaust those resources unnecessarily if they're not returned to the system promptly after use.
* Holding files open may prevent other actions being performed on them, such as moves or deletion.
* Files and sockets that are shared throughout a program may inadvertantly be read from or written to after logically being closed. If they are actually closed, attempts to read or write from them will throw exceptions, making the problem known sooner.

Furthermore, while files and sockets are automatically closed when the file object is destructed, tying the life-time of the file object to the state of the file is poor practice, for several reasons:

* There are no guarantees as to when the runtime will actually run the file's destructor. Different Python implementations use different memory management techniques, such as delayed Garbage Collection, which may increase the object's lifetime arbitrarily and indefinitely.
* Unexpected references to the file may keep it around longer than intended (e.g. in tracebacks of exceptions, inside globals, etc).

The preferred way to manage files is using the ["with"](https://docs.python.org/3/reference/compound_stmts.html#the-with-statement) statement:

```python
with open("hello.txt") as hello_file:
    for line in hello_file:
        print line
```

For file-like objects that do not support the "with" statement, use `contextlib.closing()`:

```python
import contextlib

with contextlib.closing(urllib.urlopen("https://www.python.org/")) as front_page:
    for line in front_page:
        print line
```

Legacy code using Python 2.5 may enable the "with" statement using `from __future__ import with_statement`.

## TODO Comments

Use `TODO` comments for code that is temporary, a short-term solution, or good-enough but not perfect.

`TODO`s should include the string `TODO` in all caps, followed by the name, e-mail address, or other identifier of the person who can best provide context about the problem referenced by the `TODO`, in parentheses. A colon is optional. A comment explaining what there is to do is required. The main purpose is to have a consistent `TODO` format that can be searched to find the person who can provide more details upon request. A `TODO` is not a commitment that the person referenced will fix the problem. Thus when you create a `TODO`, it is almost always your name that is given.

```python
# TODO(kl@gmail.com): Use a "*" here for string repetition.
# TODO(Zeke) Change this to use relations.
```

If your `TODO` is of the form "At a future date do something" make sure that you either include a very specific date ("Fix by November 2009") or a very specific event ("Remove this code when all clients can handle XML responses.").

## Import Formatting

Imports should be on separate lines.

```python
Yes: import os
     import sys
```

```python
No:  import os, sys
```

Imports are always put at the top of the file, just after any module comments and doc strings and before module globals and constants. Imports should be grouped with the order being most generic to least generic:

* standard library imports
* third-party imports
* application-specific imports

Within each grouping, imports should be sorted lexicographically, ignoring case, according to each module's full package path.

```python
import foo
from foo import bar
from foo.bar import baz
from foo.bar import Quux
from Foob import ar
```

## Statements

Generally only one statement per line.

However, you may put the result of a test on the same line as the test only if the entire statement fits on one line. In particular, you can never do so with `try/except` since the `try` and `except` can't both fit on the same line, and you can only do so with an `if` if there is no `else`.

```python
Yes:
  if foo: bar(foo)
```

```python
No:
  if foo: bar(foo)
  else:   baz(foo)

  try:               bar(foo)
  except ValueError: baz(foo)

  try:
      bar(foo)
  except ValueError: baz(foo)
```

## Access Control

If an accessor function would be trivial you should use public variables instead of accessor functions to avoid the extra cost of function calls in Python. When more functionality is added you can use `property` to keep the syntax consistent.

On the other hand, if access is more complex, or the cost of accessing the variable is significant, you should use function calls (following the [Naming](#naming) guidelines) such as `get_foo()` and `set_foo()`. If the past behavior allowed access through a property, do not bind the new accessor functions to the property. Any code still attempting to access the variable by the old method should break visibly so they are made aware of the change in complexity.

## Naming

`module_name, package_name, ClassName, method_name, ExceptionName, function_name, GLOBAL_CONSTANT_NAME, global_var_name, instance_var_name, function_parameter_name, local_var_name`.

### Names to Avoid

* single character names except for counters or iterators
* dashes (-) in any package/module name
* `__double_leading_and_trailing_underscore__` names (reserved by Python)

### Naming Convention

* "Internal" means internal to a module or protected or private within a class.
* Prepending a single underscore (`_`) has some support for protecting module variables and functions (not included with `import * from`). Prepending a double underscore (`__`) to an instance variable or method effectively serves to make the variable or method private to its class (using name mangling).
* Place related classes and top-level functions together in a module. Unlike Java, there is no need to limit yourself to one class per module.
* Use CapWords for class names, but lower_with_under.py for module names. Although there are many existing modules named CapWords.py, this is now discouraged because it's confusing when the module happens to be named after a class. ("wait -- did I write `import StringIO or from StringIO import StringIO?`")

### Guidelines derived from Guido's Recommendations

| Type                       | Public              | Internal                                                             |
| -------------------------- | ------------------- | -------------------------------------------------------------------- |
| Packages	                 | lower_with_under	   |                                                                      |
| Modules	                   | lower_with_under	   | \_lower_with_under                                                   |
| Classes	                   | CapWords	           | \_CapWords                                                           |
| Exceptions	               | CapWords            |	                                                                    |
| Functions	                 | lower_with_under()	 | \_lower_with_under()                                                 |
| Global/Class Constants     | CAPS_WITH_UNDER     | \_CAPS_WITH_UNDER                                                    |
| Global/Class Variables     | lower_with_under	   | \_lower_with_under                                                   |
| Instance Variables	       | lower_with_under	   | \_lower_with_under (protected) or \_\_lower_with_under (private)     |
| Method Names	             | lower_with_under()	 | \_lower_with_under() (protected) or \_\_lower_with_under() (private) |
| Function/Method Parameters | lower_with_under    |                                                                      |
| Local Variables	           | lower_with_under	   |                                                                      |

## Main

Even a file meant to be used as a script should be importable and a mere import should not have the side effect of executing the script's main functionality. The main functionality should be in a main() function.

In Python, `pydoc` as well as unit tests require modules to be importable. Your code should always check `if __name__ == '__main__'` before executing your main program so that the main program is not executed when the module is imported.

```python
def main():
      ...

if __name__ == '__main__':
    main()
```

All code at the top level will be executed when the module is imported. Be careful not to call functions, create objects, or perform other operations that should not be executed when the file is being `pydoc`ed.
