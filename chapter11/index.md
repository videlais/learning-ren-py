# Chapter 11: User Interface Statements: Interactions

- [Chapter 11: User Interface Statements: Interactions](#chapter-11-user-interface-statements-interactions)
  - [Interactions](#interactions)
    - [`bar`](#bar)
      - [Bar Input Values](#bar-input-values)
        - [**StaticValue(value=0.0, range=1.0)**](#staticvaluevalue00-range10)
        - [**VariableValue(variable, range)**](#variablevaluevariable-range)
      - [`range`](#range)
    - [`button`](#button)
      - [Button `action`](#button-action)
      - [Button `alternate`](#button-alternate)
      - [Button `hovered`](#button-hovered)
      - [Button `unhovered`](#button-unhovered)
    - [`imagebutton`](#imagebutton)
      - [`auto`](#auto)
      - [Imagebutton `action`](#imagebutton-action)
      - [Imagebutton `alternate`](#imagebutton-alternate)
      - [Imagebutton `hovered`](#imagebutton-hovered)
      - [Imagebutton `unhovered`](#imagebutton-unhovered)
    - [`input`](#input)
      - [`value`](#value)
      - [`default`](#default)
      - [`copypaste`](#copypaste)
    - [`key`](#key)
      - [Keys](#keys)
      - [`action`](#action)
    - [`mousearea`](#mousearea)
      - [`area`](#area)
      - [Mousearea `hovered`](#mousearea-hovered)
      - [Mousearea `unhovered`](#mousearea-unhovered)
    - [`textbutton`](#textbutton)
      - [Textbutton `action`](#textbutton-action)
      - [Textbutton `alternate`](#textbutton-alternate)
      - [Textbutton `hovered`](#textbutton-hovered)
      - [Textbutton `unhovered`](#textbutton-unhovered)
  - [Common Style Properties](#common-style-properties)
    - [`at`](#at)
    - [`id`](#id)
    - [`style`](#style)
    - [`style_prefix`](#style_prefix)
    - [`style_suffix`](#style_suffix)
  - [Reviewing Concepts](#reviewing-concepts)

---

## Interactions

While both containers and arrangement keywords are primarily designed to contain children, other screen language keywords are used to present interactive elements to users.

### `bar`

```Python
screen example():

    frame:
        bar
```

The keyword `bar` creates a horizontally-oriented interactive element.

#### Bar Input Values

```Python
screen example():

    frame:
        bar value
```

The `value` of a Bar can be either a fixed whole number or [one of several functions](https://www.renpy.org/doc/html/screen_actions.html#bar-values).

Two notable function for Bar values are **StaticValue()** and **VariableValue()**.

##### **StaticValue(value=0.0, range=1.0)**

```Python
screen example():

  frame:
    bar:
      value StaticValue(2, 10)
```

The [function **StaticValue(value=0.0, range=1.0)**](https://www.renpy.org/doc/html/screen_actions.html#StaticValue) uses two values, *value*, the current value, and *range*, the total value.

The user **cannot** change the value of a bar value set using **StaticValue()**.

##### **VariableValue(variable, range)**

```Python
default ValueToChange = 1

screen example():

  frame:
    bar:
      value VariableValue("ValueToChange", 10)
```

The [function **VariableValue(variable, range)**](https://www.renpy.org/doc/html/screen_actions.html#VariableValue) accepts multiple values. The first two are the name of the variable within a **String** to change and the total range.

With **VariableValue()**, any changes to the Bar will be reflected in the value of the variables within the range passed to the function.

#### `range`

```Python
screen example():

  frame:
    bar:
      value 1
      range 10
```

If `value` is set to a number, the keyword `range` can also be used to set the range of the Bar.

### `button`

```Python
screen example():

  frame:
    button
```

The keyword `button` creates a Button (clickable area).

#### Button `action`

The `action` of a Button is what should happen when the user clicks the Button.

#### Button `alternate`

The `alternative` of a Button is what should happen when a user right-clicks or otherwise does does an "alternative" interaction.

#### Button `hovered`

The `hovered` of a Button is what should happen when the Button has focus (either selected or cursor over area).

#### Button `unhovered`

The `unhovered` of a Button is what should happen when the Button loses focus (either de-selected or cursor leaves area).

### `imagebutton`

An `imagebutton` works like a `button`, but uses an image.

#### `auto`

An Imagebutton is most often used with `auto` to let Ren'Py know to use built-in keywords based on the filename of an image. Based on the interaction, `_hover` and `_idle` are used. If the Imagebutton has focus, a filename ending in `_hover` will be used. Otherwise, `_idle` will be used.

#### Imagebutton `action`

The `action` of an Imagebutton is what should happen when the user clicks.

#### Imagebutton `alternate`

The `alternative` of an Imagebutton is what should happen when a user right-clicks or otherwise does does an "alternative" interaction.

#### Imagebutton `hovered`

The `hovered` of an Imagebutton is what should happen when the Imagebutton has focus (either selected or cursor over area).

#### Imagebutton `unhovered`

The `unhovered` of a Imagebutton is what should happen when the Imagebutton loses focus (either de-selected or cursor leaves area).

### `input`

```Python
default name = ""

screen example():

    frame:
        vbox:
            text "Input Name"
            input


# The game starts here.
label start:

    call screen example
    $ name = _return
```

An `input` creates an area for text input. When ENTER is pressed, the text will be saved in the variable `_return`.

> **Note:** In order to prevent story progression, `call screen` should be used to give the screen containing the `input` focus.

#### `value`

The keyword `value` sets the value of the Input.

#### `default`

The keyword `default` defines the default value of the Input.

#### `copypaste`

The keyword `copypaste` sets if the Input should allow copying and pasting text. Accepted values are either `True` or `False`.

### `key`

The keyword `key` defines what should happen with a key is pressed. Ren'Py defines "key" loosely, as this can also include mouse events and joystick presses.

#### Keys

```Python
screen example():

    frame:
        vbox:
            key "K_BACKSPACE" action Return(None)
```

Possible keys for use with `key` include all named letters and numbers. Special keys such as BACKSPACE and TAB must be used with a `K_` prefix and in all uppercase. For example, to respond to BACKSPACE, it would be "K_BACKSPACE".

#### `action`

The `action` for a Key is what should happen when the key is pressed.

### `mousearea`

A `mousearea` is an area of the screen that can react to the cursor entering or leaving. A `mouseover` does not take focus (like an `input` might), so it is possible to have other interactive keywords within a `mousearea`.

#### `area`

The keyword `area` defines the starting x, starting y, width, and height of the `mousearea`

#### Mousearea `hovered`

The `hovered` action is what should happen when the cursor is within the `mousearea`.

#### Mousearea `unhovered`

The `unhovered` action is what should happen when the cursor leaves the `mouseover`.

### `textbutton`

```Python
screen example():

    frame:
        vbox:
            textbutton "This is a button"
```

The keyword `textbutton` creates a button containing a text label.

#### Textbutton `action`

The `action` of a Textbutton is what should happen when the user clicks the Button.

#### Textbutton `alternate`

The `alternative` of a Textbutton is what should happen when a user right-clicks or otherwise does does an "alternative" interaction.

#### Textbutton `hovered`

The `hovered` of a Textbutton is what should happen when the Textbutton has focus (either selected or cursor over area).

#### Textbutton `unhovered`

The `unhovered` of a Textbutton is what should happen when the Textbutton loses focus (either de-selected or cursor leaves area).

## Common Style Properties

### `at`

The `at` keyword applies a transform, a list of transformations, or keywords to create a transforms as defined in the Animation and Transformation Language (ATL) language in Ren'Py.

### `id`

All interactable screen language keywords can have their own `id`. This must be a **String** value and must, therefore, be enclosed in quotation marks.

### `style`

The keyword `style` keyword specifies which built-in or defined style should be applied to the displayable.

> The built-in styles included with the visual novel are defined in the `screens.rpy` file. These include styles like "input" and "button" that define the default presentation for the built-in displayables in Ren'Py.

### `style_prefix`

The keyword `style_prefix` defines the prefix to be applied to the existing or defined `style` of the displayable. For example, if the style "pref_vbox" is defined and the keyword `vbox` is used with the `style_prefix` "pref", that built-in style would be used.

The style prefix is applied to both the displayable *and* all of its children.

### `style_suffix`

The keyword `style_suffix` defines the suffix to be applied to the existing `style` and `style_prefix` of the displayable. In the case of the `style` "vbox", the `style_prefix` "pref", and `style_suffix` is "button", the combined name would be "pref_vbox_button".

The style suffix is only applied to the displayable and *not* its children.

## Reviewing Concepts

Ren'Py defines various keywords for creating interactions with users. These are `bar`, `button`, `textbutton`, `imagebutton`, `input`, `key`, and `mousearea`.

Each interactable keyword has their own keywords but also share properties describing style prefixes and suffixes.
