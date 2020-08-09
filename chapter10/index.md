# Chapter 10: User Interface Statements: Containers and Arrangements

- [Chapter 10: User Interface Statements: Containers and Arrangements](#chapter-10-user-interface-statements-containers-and-arrangements)
  - [Containers](#containers)
    - [Keywords](#keywords)
      - [`fixed`](#fixed)
      - [`frame`](#frame)
      - [`viewport`](#viewport)
      - [`window`](#window)
    - [Identification](#identification)
  - [Arrangements](#arrangements)
    - [`hbox`](#hbox)
    - [`vbox`](#vbox)
    - [`grid`](#grid)
    - [`vpgrid`](#vpgrid)
    - [Style Properties](#style-properties)
      - [Box Style Properties](#box-style-properties)
      - [Box `spacing`](#box-spacing)
        - [`first_spacing`](#first_spacing)
        - [`box_reverse`](#box_reverse)
        - [`box_wrap`](#box_wrap)
        - [`box_wrap_spacing`](#box_wrap_spacing)
      - [Grid Style Properties](#grid-style-properties)
        - [Grid `spacing`](#grid-spacing)
        - [`xspacing`](#xspacing)
        - [`yspacing`](#yspacing)
  - [Position Style Properties](#position-style-properties)
    - [`xpos` and `ypos`](#xpos-and-ypos)
    - [`xanchor` and `yanchor`](#xanchor-and-yanchor)
    - [`xalign` and `yalign`](#xalign-and-yalign)
    - [`xmaximum` and `ymaximum`](#xmaximum-and-ymaximum)
    - [`xfill`and `yfill`](#xfilland-yfill)
  - [Common Style Properties](#common-style-properties)
    - [`at`](#at)
    - [`id`](#id)
    - [`style`](#style)
    - [`style_prefix`](#style_prefix)
    - [`style_suffix`](#style_suffix)
  - [Reviewing Concepts](#reviewing-concepts)

---

Within screens, displayables are organized through using container and arrangement keywords.

## Containers

Each container keyword specifies how its contents should be presented to the user. These define sub-sections of code within a screen are indented in the same way.

> In Ren'Py *containers* are used with special keywords to describe how one or more displayables are shown to a user

### Keywords

#### `fixed`

```Python
screen fixed_example():
  fixed:
    text "Example"
```

When no container keyword is specified, the keyword `fixed` is applied. This defines a "fixed" area for the screen.

A fixed screen does not have a border or background. It is merely a "fixed" portion shown to the user.

#### `frame`

```Python
screen fixed_example():
  frame:
    text "Example"
```

Unlike `fixed`, the keyword `frame` defines a border around the displayables within the screen. It will use whatever background color is specified in the current color palette.

#### `viewport`

```Python
screen fixed_example():
  viewport:
    text "Example"
```

The [keyword `viewport`](https://www.renpy.org/doc/html/screens.html#viewport) defines a "fixed" portion like the keyword `fixed`, but allows for using scroll-bars for horizontal and vertical access.

If the displayables within the viewport extend past the current viewing area, the scroll-bars can be used to show the contents beyond what is currently shown to the user.

#### `window`

```Python
screen window_example():
    window:
        # Show as part of the textbox
        text "Example"
```

The keyword `window` is used to display dialogue to the user. It defaults to using the same area as the textbox (where the name and dialogue of a character is normally shown).

### Identification

```Python
screen multiple_example():
  fixed id "fixed":
    text "First example"

  fixed id "fixed2":
    text "Second example"
```

Screens can use multiple containers. In order to avoid possible conflict between containers, the keyword `id` can be used to give each an unique identification name. These are written using a **String** value (enclosed in quotations) after the use of the keyword `id`.

Because these identifications are **String** values, this means they can contain spaces and other special symbols. As long as they are within the quotation marks, they can be used as part of its identification.

## Arrangements

Within screens, displayables can be arranged using a special set of keywords. These affect whatever is "in" them.

Arrangement keywords are used within containment keywords. If an arrangement keyword is used within a specific containment keyword, `fixed` is used by default.

### `hbox`

```Python
screen example():
  fixed:
    hbox:
      text "First entry"
      text "Second entry"
```

The `hbox` keyword arranges displayables horizontally. Any additional displayable within a `hbox` is added next to the previous one along a horizontal line.

### `vbox`

```Python
screen example():
  fixed:
    vbox:
      text "First entry"
      text "Second entry"
```

The `vbox` keyword arranges displayables vertically. Any additional displayable within a `vbox` is added next to the previous one along a vertical line.

### `grid`

```Python
screen example():
  fixed:
    grid 2 2:
      text "First entry"
      text "Second entry"
      text "Third entry"
      text "Fourth entry"
```

The keyword `grid` combines the presentation of `hbox` and `vbox`. It uses two numbers that define the rows and column of the grid.

For example, to define a 2x2 grid, the numbers 2 and 2 can be used to describe how many rows and columns.

### `vpgrid`

```Python
screen example():
    fixed:
        vpgrid:

            rows 2
            cols 2

            text "First entry"
            text "Second entry"
            text "Third entry"
            text "Fourth entry"
```

Like the `viewport` keyword for containing displayables, the keyword `vpgrid` combines a `grid` with a `viewport` for displayables. However, instead, of using numbers after the keyword `grid`, it uses extra keywords for defining its rows and columns.

The keywords `rows` and `cols` define the rows and columns for the `vpgrid`.

### Style Properties

All containment and arrangement keywords have style properties. These define how they are shown and in relation to each other.

#### Box Style Properties

Used with `hbox` and `vbox`, the box style properties define how displayables are arranged within boxes.

#### Box `spacing`

```Python
screen example():
  fixed:
    hbox:

      spacing 5

      text "First entry"
      text "Second entry"
```

The keyword `spacing` defines the spacing between displayables in pixels. Spacing must be expressed in whole numbers.

##### `first_spacing`

```Python
screen example():
  fixed:
    vbox:

      first_spacing 5

      text "First entry"
      text "Second entry"
```

The keyword `first_spacing` defines the spacing between the first and second displayables within the box, in pixels. Spacing must be expressed in whole numbers.

##### `box_reverse`

```Python
screen example():
  fixed:
    hbox:

      box_reverse True

      # This will be second
      text "First entry"
      # This will be first
      text "Second entry"
```

The keyword `box_reverse` defines placement of displayables. If set to `True`, displayables will be arranged in reverse order. For a hbox, this is right-to-left. For vbox, bottom-to-top. Its default value is `False`.

##### `box_wrap`

```Python
screen example():
  fixed:
    hbox:

      # Wrap the contents
      box_wrap True
      # Set a maximum of 300 pixels (to force wrap)
      xmaximum 300

      text "First entry"
      text "Second entry"
      text "Third entry"
```

The keyword `box_wrap` defines if displayables should wrap on line or column. If set to `True`, displayables will wrap. If set to `False`, which is the default, displayables will not wrap.

> **Note:** This example also uses the keyword `xmaximum` to force a horizontal wrapping of its contents.

##### `box_wrap_spacing`

```Python
screen example():
  fixed:
    hbox:

      # Wrap the contents
      box_wrap True
      # Set a maximum of 300 pixels (to force wrap)
      xmaximum 300
      # Add 20 pixels before wrapping
      box_wrap_spacing 20

      text "First entry"
      text "Second entry"
      text "Third entry"
```

The keyword `box_wrap_spacing` defines the spacing between wrapped lines or columns in pixels. It will only be used if `box_wrap` is also set to `True`.

#### Grid Style Properties

Used with `grid` and `vpgrid`, the grid style properties define how displayables are arranged within grids.

##### Grid `spacing`

```Python
screen example():
  fixed:
    grid 2 2:
        # Spacing of 15 pixels between rows and columns
        spacing 15
        # Text displayables
        text "First entry"
        text "Second entry"
        text "Third entry"
        text "Fourth entry"
```

The keyword `spacing` defines the spacing between displayables in pixels. Spacing must be expressed in whole numbers.

##### `xspacing`

```Python
screen example():
  fixed:
    grid 2 2:
        # Spacing of 15 pixels between rows
        xspacing 15
        # Text displayables
        text "First entry"
        text "Second entry"
        text "Third entry"
        text "Fourth entry"
```

The keyword `xspacing` defines the horizontal spacing between displayables in pixels. Spacing must be expressed in whole numbers or `None`. This property takes precedence over the `spacing` property.

##### `yspacing`

```Python
screen example():
  fixed:
    grid 2 2:
        # Spacing of 15 pixels between columns
        yspacing 15
        # Text displayables
        text "First entry"
        text "Second entry"
        text "Third entry"
        text "Fourth entry"
```

The keyword `yspacing` defines the vertical spacing between displayables in pixels. Spacing must be expressed in whole numbers or `None`. This property takes precedence over the `spacing` property.

## Position Style Properties

Both container and arrangement keywords can be positioned in different ways.

### `xpos` and `ypos`

```Python
screen example():
    frame:
        # Position x to 200
        xpos 200
        # Position y to 200
        ypos 200

        text "I'm at 200, 200!"
```

The keywords `xpos` and `ypos` define the starting position, relative to the left side of the element.

### `xanchor` and `yanchor`

```Python
screen example():
    frame:
        # Position x anchor to 20
        xanchor 20
        # Position y anchor to 20
        yanchor 20

        text "I'm anchored at 20, 20!"
```

The position anchor of the x, `xanchor`, and y, `yanchor` relative to the left side of the displayable. This will becomes the new anchor (starting point) of the displayable.

### `xalign` and `yalign`

```Python
screen example():
    frame:
        # X-Align at 50%
        xalign 0.5
        # Y-Align at 50%
        yalign 0.5

        text "Aligned in the very center!"
```

Sets the position (`xpos` or `ypos`) and anchor (`xanchor` or `yanchor`) in relation to the screen starting with 0.0 for leftmost and 1.0 for rightmost sides.

### `xmaximum` and `ymaximum`

```Python
screen example():
    frame:
        # Set xmaximum to 200
        xmaximum 200
        # Set ymaximum at 200
        ymaximum 200

        text "Size of 200x200!"
```

Set the maximum horizontal (`xmaximum`) and vertical (`ymaximum`) size of the displayable in pixels.

### `xfill`and `yfill`

```Python
screen example():
    frame:
        xfill True

        text "Fill horizontally"
```

The keywords `xfill` and `yfill` sets if the displayable should extend to fill the horizontal or vertical space. If `True`, it will extend. If `False`, it will not. `xfill` and `yfill` will only work on displayables that can change shape.

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

*Containers* (`fixed`, `frame`, `viewport`, and `window`) are abstract ways to group displayables in Ren'Py. A set of keywords (`hbox`, `vbox`, `grid` and `vpgrid`) can be used to arrange displayables within containers.

Style properties can be used to change how container and arrangement keywords work and are presented to users.

Both container and arrangement keywords can be positioned through their own set of keywords.
