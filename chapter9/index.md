# Screens and Screen Language

- [Screens and Screen Language](#screens-and-screen-language)
  - [Screen Language](#screen-language)
    - [`screen`](#screen)
    - [`modal`](#modal)
    - [`tag`](#tag)
    - [`zorder`](#zorder)
    - [`variant`](#variant)
  - [Showing, Hiding, and Calling Screens](#showing-hiding-and-calling-screens)
    - [Showing](#showing)
    - [Hiding](#hiding)
    - [Calling](#calling)
  - [Reviewing Concepts](#reviewing-concepts)

---

## Screen Language

Everything that happens in Ren'Py happens as part of a *screen*. The Main Menu, all narration and dialogue, and even loading and saving games happens on their own screens. In general terms, then, a screen is way to group other displayables together.

> A *screen* is an abstraction within Ren'Py for organizing displayables.

Each screen is, itself, also a displayable. This means that it can be treated as a displayable and used with other, existing keywords like `show`.

Ren'Py has a special set of keywords for describing screens called its *screen language*. This is its own scripting language. Like with `scene` and `show` as they apply to images, the keywords used in the screen language describe how displayables are arranged and shown.

### `screen`

Screens are defined using the `screen` keyword. These work like functions, but use screen language to describe what should be displayed and how.

```Python
# Create a screen
screen hello_world():
    text "Hello world"
```

The keyword `screen` precedes its name. Like with other variables and variable-like entries in Ren'Py, the name of the screen must follow the same naming rules: they can only contain letters, numbers, and the underscore. They cannot contain special symbols or spaces.

Screen, like labels, work as their own sections of code. Their names are followed by a colon and all other keywords that appear within the screen's code are indented under it.

Like variables, multiple screens cannot have the same name.

```Python
# Create a screen
screen hello_world():
    text "Hello world"
```

In the above code, for example, the screen is named `hello_world()` and it contains one: `text "Hello world"`.

### `modal`

```Python
screen hello_world():
  # Set modal to True (default is False)
  modal True
```

The keyword `modal` defines if the screen is a *modal* or not. It accepts either `True` or `False` values.

In user interface terms, a *modal* is a window or window-like screen that is "above" all other displayables. When the `modal` keyword is set to `True`, this will prevent any screens or other displayables "under" it from being interacted with due to its modal status.

### `tag`

```Python
screen hello_world():
  # Screen is part of the tag "example"
  tag example
```

Like with images, screens can also be organized through tags. In the case of screens, the keyword `tag` is used to categorize screens. **Screens of the same tag will replace each other.**

Tags follow the same rules as variables: they can contain letters, numbers, and the underscore. They cannot contain special symbols or spaces.

### `zorder`

```Python
screen hello_world():
  # Set zorder to 10 (drawer "closer" than than the default of 0)
  zorder 10
```

The keyword `zorder` defines how close to the user the screen should be displayed as a whole number. In the case of multiple screens being shown at the same time, the screen with the higher `zorder` number will appear "on top" of the others, being drawn closer to the user.

By default, `zorder` is set to 0.

### `variant`

```Python
screen hello_world():
  # Show on large screens
  variant "large"

screen hello_world():
  # Show on small screens
  variant "small"
```

Normally, screens cannot share names. However, the keyword `variant` allows for defining screens for *variants*, different device and display settings. If the visual novel is being built for a specific device, or the special variable `RENPY_VARIANT` is set, Ren'Py will only use screens matching the selected variant available for that device. In the case of "android", for example, this might be the variants "android touch mobile small None".

> **Note:** The available variants for any device can be set using the [`config.variants` variable](https://www.renpy.org/doc/html/config.html#var-config.variants).

Available Variants Include:

- "large"
- "medium"
- "small"
- "tablet"
- "phone"
- "touch"
- "tv"
- "ouya"
- "firetv"
- "android"
- "ios"
- "mobile"
- "pc"
- "web"
- None

The variant `None` is always included. This is the fallback if no other variants were found or otherwise detected.

## Showing, Hiding, and Calling Screens

Screens are displayables. This means they can be shown, hidden, and used in different ways. Unlike other displayables, however, screens are also *function* in Ren'Py. This means they can accept data (parameters) and even return results.

While defining screens takes place as part of initialization, showing, hiding, and calling screens takes place as part of the `label start`.

### Showing

The `show` keyword is used to display screens in Ren'Py. Unlike working with images, screens are shown with the pair of keywords, `show screen`, followed by the name of the screen to show.

```Python

# Initialization

# Create a screen
screen hello_world():
  text "Hello world"

# Script of visual novel
label start:
  show screen hello_world
```

The keywords `show screen` **must** be used as part of the script of a visual novel. They cannot be used as part of initialization.

### Hiding

The keyword `hide` hides a name displayable. As screens are, themselves, displayables, this means screens can also be hidden (if they were previously being shown).

Like with the keyword pairs of `show screen`, the `hide` keyword is also used with `screen`. In order to hide a screen, the keywords `hide screen` must be used with an existing screen name.

```Python
# Script of visual novel
label start:
  hide screen hello_world
```

The keywords `hide screen` follow the same rules as `show screen`. They **must** be used as part of the script of the visual novel and not as part of the initialization.

### Calling

In Ren'Py, screens are *functions*. This means they can be "called."

> In programming terminology, a function is "called" when its name is used followed by opening and closing parentheses. Data can also be passed to the function as parameters inside the parentheses and separated by commas. Any result of the calling is its output. In Ren'Py, these value is storied in a special variable called `_return`.

It is possible to "call" a screen through the keywords `call screen`. Unlike the usage of `show screen` and `hide screen`, the keywords `call screen` expect to see opening and closing parentheses after the name of the screen if data is being passed to the screen. This data is parameters and matches its arguments. Any variables defined as part of its arguments can be used inside of the screen.

```Python
screen hello(name):
  # Show the text of "Hi, " combined with whatever name is passed to the screen
  text "Hi, " + name
  # Show a textbutton
  # When it is clicked (its action), use Return() to return control
  textbutton "Return Control" action Return()

# The game starts here.
label start:
  # Call the screen hello() and pass it "Dan" as the parameter name
  call screen hello(name = "Dan")
```

Unlike showing screens, control passed to the screen when called. This means that an action must be taken to "return" control back to the script.

> Working with interactions and the `action` keyword are explained more in the following chapters.

## Reviewing Concepts

A *screen* is a way to group displyables together. Screens are defined using the `screen` keyword. Screens are functions in Ren'Py.

Screens use the keywords `modal`, `tag`, `zorder`, and `variant` to describe themselves in relation to the user and other screens. To prevent other screens and displayables from being using while the screen is being shown, the keyword `modal` can be used. To help group screens, the keyword `tag` is used.

`zorder` describes how "close" to draw a screen. The higher the number, the higher the screen. If one or more screens are shown to a user at the same time, the screen with the largest `zorder` value will be shown "on top" of the others.

The keyword `variant` is used to define multiple screens and then have Ren'Py decide if to show it based on the device or resolution when the visual novel is run. They are a large number of options for variants with the default, `None`, always defined.

Screens are functions in Ren'Py. This means they can accept data, parameters, and optionally return results. If a screen returns some data, it is part of the special variable `_return` in Ren'Py.
