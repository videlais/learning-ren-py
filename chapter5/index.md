# Chapter 5: Transitions

- [Chapter 5: Transitions](#chapter-5-transitions)
  - [Displayables](#displayables)
  - [`with` keyword](#with-keyword)
  - [Common Transitions](#common-transitions)
    - [`fade`](#fade)
    - [`dissolve`](#dissolve)
  - [Custom Transitions](#custom-transitions)
    - [Using Time](#using-time)
    - [Defining Transitions](#defining-transitions)
  - [Reviewing Concepts](#reviewing-concepts)

---

## Displayables

In Chapter 4, images were discussed. Used with the keywords `scene` and `show`, images were searched for in the `images` folder based on their tags and attributes. Depending on the usage, other, existing images were either removed and completely replaced (`scene`) or added (`show`). In the cases where the tags matched but the attribute did not, `show` would replace the existing image.

Images are part of a larger abstraction called *displayables* in Ren'Py. These include **anything** that can be displayed, including images.

> *Displayables* are anything that can be displayed in Ren'Py. These include images, menus, and even colors.

Understanding displayables is important because *transitions* can be applied to them. Anything that can be displayed (all displayables) can be affected in how they are shown to a player.

> A *transition* in Ren'Py defines how it is shown to a player. Depending on the keyword, it may be shown quickly or over time using a certain effect as associated with a particular keyword.

In Ren'Py, transitions are applied to images (and other displayables) using the keyword `with`. It should follow the use of `scene` or `show` and affects how those images are presented.

## `with` keyword

Open the Ren'Py Launcher. Select *The Question*.

Click on "script.rpy" under Edit File. This will open the file in Atom.

Look at Lines 17-19:

```Python
scene bg lecturehall
with fade
```

The above code is an example of a transition. On the line after the use of `scene` or `show`, the keyword `with` is used. When played, the pairing of `with fade` will apply that transition to the use of the keyword `scene`.

> The keyword `with` applies a transition to a displayable.

As was discussed in an earlier chapter, the `scene` keyword removes all current displayables (previously explained as "images") on the master layer. Next, it replaces that content with the new image and applies the associated transition with its own keyword.

The application of the transition, as with its placement in the code, is used "with" the last operation. First, `scene` removes the existing displayables. Second, it applies the transition. As both `scene` and `show` "display" things, any use of a transition affects how it shows things as they come "into" its displaying, not when removed.

## Common Transitions

The visual novel *The Question* shows off two of the most common transitions in Ren'Py: `fade` and `dissolve`.

> The keywords `fade` and `dissolve` are two built-in transitions in Ren'Py. There are [many others](https://www.renpy.org/doc/html/transitions.html).

### `fade`

The most common transition in Ren'Py is using the keyword `fade`. When used with the keyword `with`, this "fades" in the image, applying first a black background and then slowly shows the image.

In *The Question*, it appears in multiple places.

It appears first on Lines 17-19 in combination with the `scene` keyword. (This is applied, again, to the image appearing and not the removal of other displayables.)

```Python
scene bg lecturehall
with fade
```

*The Question* uses the keyword `fade` with transitions between scenes. For characters, it uses a different transition: `dissolve`.

### `dissolve`

In *The Question*, the keyword `dissolve` is used in multiple places with the keyword `show`. In these cases *The Question* has multiple examples of where this keyword is used well: shifting between images based on their attributes. In these case, the character changes their reactions and the dissolve is used when it changes.

In *The Question*, this first appears on Lines 33-34:

```Python
show sylvie green normal
with dissolve
```

Like with `fade`, the use of `dissolve` is often (but not always) used for character reactions changes. The major exception of this appears on Lines 163-164:

```Python
scene black
with dissolve
```

As was explained in a previous chapter, the use of the `black` keyword is a special color. When used with a transitions, as it is here, it transitions to a black screen.

This particular combination appears multiple times in *The Question*. In each case, it is transitioning between tone within the "scene" in which it appears.

## Custom Transitions

All transitions are actually [functions behind-the-scenes](https://www.renpy.org/doc/html/transitions.html). This means that they accept arguments and their effects can be changed through giving them extra values. All transitions with keywords are special versions of these functions pre-built for usage in Ren'Py.

> The built-in keyword transitions are used in all lowercase. When using the function version, the first letter is capitalized and followed by opening and closing parentheses.

### Using Time

The most common argument to a transition is how long it should run. In other words, *time*.

Using the [**Dissolve()** function](https://www.renpy.org/doc/html/transitions.html#Dissolve), for example, might look like the following:

```Python
with Dissolve(5.0)
```

The [**Fade()** function](https://www.renpy.org/doc/html/transitions.html#Fade) can accept multiple time values.

```Python
with Fade(0.5, 0.0, 0.5)
```

### Defining Transitions

Used as *transition classes*, the functions return **Transition** objects like the **Character()** method does for **Character**. In the same way, they must be used with the keyword `define` to create a custom transition with new values.

An example of a transition named **Example()** might look like the following:

```Python
define exampleTransition = Example(some, values)
```

In the above case, the new **Transition** is saved in the variable `exampleTransition`. It would be used like any other transition using the keyword `with`.

```Python
show image
with exampleTransition
```

> **Reminder:** All uses of the keyword of `define` should happen *before* the start of the script (with `label start`).

## Reviewing Concepts

In Ren'Py, anything that can be displayed is a *displayable*. Images and other things are in this category.

*Transitions* define how displayables are presented to a player. There are [many built-in](https://www.renpy.org/doc/html/transitions.html) keywords, but `fade` and `dissolve` are common.

The keyword `with` applies a transition to a displayable. It can be combined with custom usages or definitions of transition functions. In these case, it is treated as a function with a capital letter and open and closing parentheses around any arguments used.
