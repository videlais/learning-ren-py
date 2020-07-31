# Chapter 6: Variables and Conditionals

- [Chapter 6: Variables and Conditionals](#chapter-6-variables-and-conditionals)
  - [Constants and Changing Values](#constants-and-changing-values)
    - [Reviewing `define`](#reviewing-define)
    - [Introducing `default`](#introducing-default)
    - [Ren'Py Store](#renpy-store)
  - [Working with Python Code](#working-with-python-code)
    - [Code Statements](#code-statements)
    - [Boolean Values](#boolean-values)
    - [Mathematics](#mathematics)
  - [Testing Values](#testing-values)
    - [Checking Ranges](#checking-ranges)
  - [Reviewing Concepts](#reviewing-concepts)

---

## Constants and Changing Values

There are two general storage options for variables in programming: constants, and values that can change. In Ren'Py, these are created using different keywords.

### Reviewing `define`

Starting in Chapter 2, the keyword `define` was introduced. It was used with the **Character()** method to create and save **Character** objects. These were created with the method and were "defined" using the keyword `define`.

```Python
define m = Character(_("Me"), color="#c8c8ff")
```

In Ren'Py, any values saved with the `define` keyword are treated as *constant* values. In programming terminology, a *constant* is a value that, once created, will not be changed while a program runs.

> A *constant* is a type of programming storage where its value cannot be changed after being created.

In the previous chapters, characters, once created, were not changed. During the story, they were used only as the variable before the dialogue they were to speak. They were *constant* in the story. This is the correct, and common, usage of the keyword `define`.

### Introducing `default`

Open the Ren'Py Launcher. With *The Question* selected, click on "script.rpy" under Edit File. This will open the file in Atom.

Look at Lines 6-8:

```Python
# This is a variable that is True if you've compared a VN to a book, and False
# otherwise.
default book = False
```

Unlike the use of `define`, this is a different keyword: `default`. The `define` keyword creates a constant value, one that does not change. Variables created with the `default` keyword, on the other hand, *can* be changed.

Look at Line 137:

```Python
$ book = True
```

After being created earlier in the file, on Line 137, the variable `book` is changed. This is the usage of the keyword `default` in creating it. Because it is not a constant, it can be changed.

In Ren'Py terminology, variables created with the keyword `default` are called *flags*. These are variables whose values can be changed.

> *Flags* are variables that can be changed while a visual novel is running.

In visual novels, flags are often used to check if certain events or menu options have been chosen by the user. They can be tested and different narration or dialogue lines shown to the player as a result.

### Ren'Py Store

All variables (those created with `define` *and* `default`) are part of a single *store* in Ren'Py. This is shared across all variables. This means that they **cannot** have the same name. Variables must be unique within the store and thus in the visual novel itself.

They can have the same values, but their names must be different.

> A *store* is a collection of unique entries. In Ren'Py, all variables are part of the same store and thus cannot have the same names.

## Working with Python Code

The keywords `define` and `default` can only be used *before* the `start` label. This is the *initialization* section of the file and program. Anything used here are "initialized" (setup) before the start of the visual novel.

> The *initialization* of a visual novel happens before the `label start`. Any variables used in the story must be created before they can be used.

### Code Statements

In programming terminology, a *statement* is a single line of code. It takes its name from the word itself: it "states" something.

In Ren'Py, a single line of Python code, a *statement*, must start with the dollar sign, `$`.

Look at Line 137 in *The Question*:

```Python
$ book = True
```

The above example is Python code that changes the variable `book` into a new value. (Because it was created using the keyword `default`, this is allowed.)

The use of the dollar sign, `$`, marks it as a single Python statement. In Ren'Py, the values of variables (flags) can be changed using the same pattern. This is the *only* way they can be changed.

### Boolean Values

The first few lines of *The Question* use the method **Character()** and the keyword `define`.

Look at Lines 1-4 of *The Question*:

```Python
# Declare characters used by this game.
define n = Character(_("Nathan"), color="#ff191c")
define s = Character(_("Georgia"), color="#ea4c16")
define m = Character(_("Me"), color="#c8c8ff")
```

In each case, the variables have the value of a **Character**.

Look at Line 8:

```Python
default book = False
```

This is a different value: `False`. This is an example of a *Boolean* value.

In programming terminology, Boolean values can either be `True` or `False`. That's it. They are limited to only those two values.

> Boolean values can either be `True` or `False`

Boolean values are important because they can easily be tested.

### Mathematics

In the code from *The Question*, only Boolean value are used. However, it is also possible to use numbers and perform mathematics.

Consider the following code example:

```Python
default money = 5

# The game starts here.
label start:

  $ money = money + 3
```

In the above code, the variable `money` is created. Because the keyword `default` is used, its value can be changed. After that, once the story starts, its initial value is increased by 3.

In Python, such an operation is so common that a shorthand is also possible: `+=`. In the cases where an existing value is added to itself, this would achieve the same outcome. The previous code could use this shorthand.

```Python
default money = 5

# The game starts here.
label start:

  $ money += 3
```

## Testing Values

Look at Line 173 in *The Question*:

```Python
if book:
```

The variable (flag) was created on Line 8. If the "book" label is access, its value is changed on Line 137. On Line 173, this is finally tested.

The keyword `if` tests values. If the result is `True`, the code "under" the keyword will be run. In programming terminology, this is known as a *conditional statement*. If the condition is `True`, its code will be run.

> The keyword `if` tests conditional statements. If the test is `True`, its code will be run.

If the value of the variable (flag) `book` is `True`, the visual novel will show the narration of the dialogue inside of it.

Look at Lines 173-175:

```Python
if book:

  "Our first game is based on one of Sylvie's ideas, but afterwards I get to come up with stories of my own, too."
```

In *The Question*, if the value of the variable (flag) is `True` when the story reaches this point, Line 175 will be shown. Otherwise, it will be ignored.

### Checking Ranges

The use of the `if` keyword can also test ranges of values. Instead of testing if a value is `True` or not, it can also test if a value is greater-than or less-than a value.

Consider the following example of using less-than symbol (`<`):

```Python
default example = 5

# The game starts here.
label start:

    if example < 10:

        "Show this!"
```

In the above code, the variable (flag) of `example` is created. Next, once the visual novel starts, the narration "Show this!" will be shown.

The condition is `example < 10`. The keyword `if` tests if the value of the variable of `example` is less-than the value 10. In this example, it is, and show the line of narration will be shown.

Consider the following example of using the greater-than symbol (`>`):

```Python
default example = 5

# The game starts here.
label start:

    if example > 4:

        "Show this!"
```

## Reviewing Concepts

In Ren'Py, the keyword `define` is used to create *constants*. These are values that do not change when a visual novel runs.

The keyword `default` creates variables whose values can changed. In Ren'Py, these are sometimes called *flags*

Any variables created using `define` and `default` are part of a *store* in Ren'Py. As all variables are part of the same store, none can share the same name. They must be unique.

The first part of the `script.rpy` file is used for *initialization*. Any variables needed in the story must be created before `label start`.

In Ren'Py, because it is based on Python, it supports Boolean value. There are either `True` or `False`.

The keyword `if` is used to test values as part of *conditional statements*. These can be single variables, in the case of flags, or testing for ranges using greater-than or less-than symbols with numerical values.
