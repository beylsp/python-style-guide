# Python Language Rules

## Table of Contents

  1. [Lint](#lint)
  1. [Imports](#imports)
  1. [Packages](#packages)
  1. [Exceptions](#exceptions)
  1. [Global variables](#global-variables)

## Lint

Run `pylint` over your code.

### Definition

pylint is a tool for finding bugs and style problems in Python source code. It finds problems that are typically caught by a compiler for less dynamic languages like C and C++. Because of the dynamic nature of Python, some warnings may be incorrect; however, spurious warnings should be fairly infrequent.

### Pros

Catches easy-to-miss errors like typos, using-vars-before-assignment, etc.

### Cons

`pylint` isn't perfect. To take advantage of it, we'll need to sometimes: a) Write around it b) Suppress its warnings or c) Improve it.

### Decision

Make sure you run `pylint` on your code. Suppress warnings if they are inappropriate so that other issues are not hidden.

To suppress warnings, you can set a line-level comment:

```python
dict = 'something awful'  # Bad Idea... pylint: disable=redefined-builtin
```

pylint warnings are each identified by a alphanumeric code (`C0112`) and a symbolic name (`empty-docstring`). Prefer the symbolic names in new code or when updating existing code.

If the reason for the suppression is not clear from the symbolic name, add an explanation.

Suppressing in this way has the advantage that we can easily search for suppressions and revisit them.

You can get a list of pylint warnings by doing `pylint --list-msgs`. To get more information on a particular message, use `pylint --help-msg=C6409`.

Prefer `pylint: disable` to the deprecated older form `pylint: disable-msg`.

Unused argument warnings can be suppressed by using "_" as the identifier for the unused argument or prefixing the argument name with "unused_". In situations where changing the argument names is infeasible, you can mention them at the beginning of the function. For example:

```python
def foo(a, unused_b, unused_c, d=None, e=None):
    _ = d, e
    return a
```

## Imports

Use `import`s for packages and modules only.

### Definition

Reusability mechanism for sharing code from one module to another.

### Pros

The namespace management convention is simple. The source of each identifier is indicated in a consistent way; `x.Obj` says that object `Obj` is defined in module `x`.

### Cons

Module names can still collide. Some module names are inconveniently long.

### Decision

Use `import x` for importing packages and modules. 
Use `from x import y` where `x` is the package prefix and `y` is the module name with no prefix. 
Use `from x import y as z` if two modules named `y` are to be imported or if `y` is an inconveniently long name.

For example the module `sound.effects.echo` may be imported as follows:

```python
from sound.effects import echo
...
echo.EchoFilter(input, output, delay=0.7, atten=4)
```

Do not use relative names in imports. Even if the module is in the same package, use the full package name. This helps prevent unintentionally importing a package twice.

## Packages

Import each module using the full pathname location of the module.

### Pros

Avoids conflicts in module names. Makes it easier to find modules.

### Cons

Makes it harder to deploy code because you have to replicate the package hierarchy.

### Decision

All new code should import each module by its full package name.

Imports should be as follows:

```python
# Reference in code with complete name.
import sound.effects.echo

# Reference in code with just module name (preferred).
from sound.effects import echo
```

## Exceptions

Exceptions are allowed but must be used carefully.

### Definition

Exceptions are a means of breaking out of the normal flow of control of a code block to handle errors or other exceptional conditions.

### Pros

The control flow of normal operation code is not cluttered by error-handling code. It also allows the control flow to skip multiple frames when a certain condition occurs, e.g., returning from N nested functions in one step instead of having to carry-through error codes.

### Cons

May cause the control flow to be confusing. Easy to miss error cases when making library calls.

### Decision

Exceptions must follow certain conditions:

* Raise exceptions like this: `raise MyException('Error message')` or `raise MyException`. Do not use the two-argument form (`raise MyException, 'Error message'`) or deprecated string-based exceptions (`raise 'Error message'`).
* Modules or packages should define their own domain-specific base exception class, which should inherit from the built-in Exception class. The base exception for a module should be called `Error`.

```python
class Error(Exception):
    pass
```

* Never use catch-all `except:` statements, or `catch Exception` or `StandardError`, unless you are re-raising the exception or in the outermost block in your thread (and printing an error message). Python is very tolerant in this regard and `except:` will really catch everything including misspelled names, sys.exit() calls, Ctrl+C interrupts, unittest failures and all kinds of other exceptions that you simply don't want to catch.
* Minimize the amount of code in a `try/except` block. The larger the body of the try, the more likely that an exception will be raised by a line of code that you didn't expect to raise an exception. In those cases, the `try/except` block hides a real error.
* Use the `finally` clause to execute code whether or not an exception is raised in the `try` block. This is often useful for cleanup, i.e., closing a file.
* When capturing an exception, use `as` rather than a comma. For example:

```python
try:
    raise Error
except Error as error:
    pass
```

## Global variables

Avoid global variables.

### Definition

Variables that are declared at the module level.

### Pros

Occasionally useful.

### Cons

Has the potential to change module behavior during the import, because assignments to module-level variables are done when the module is imported.

### Decision

Avoid global variables in favor of class variables. Some exceptions are:

* Default options for scripts.
* Module-level constants. For example: `PI = 3.14159`. Constants should be named using all caps with underscores; see [Naming](https://github.com/beylsp/python-style-guide/blob/master/README.md#naming).
* It is sometimes useful for globals to cache values needed or returned by functions.
* If needed, globals should be made internal to the module and accessed through public module level functions; see [Naming](https://github.com/beylsp/python-style-guide/blob/master/README.md#naming).



