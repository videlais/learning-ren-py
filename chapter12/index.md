# Chapter 12: Screen Language: Actions and Control Statements

- [Chapter 12: Screen Language: Actions and Control Statements](#chapter-12-screen-language-actions-and-control-statements)
  - [Actions](#actions)
    - [Control](#control)
      - [**Call(label)**](#calllabel)
      - [**Hide(screen, transition=None)**](#hidescreen-transitionnone)
      - [**Jump(label)**](#jumplabel)
      - [**NullAction()**](#nullaction)
      - [**Return(value=None)**](#returnvaluenone)
      - [**Show(screen, transition=None)**](#showscreen-transitionnone)
    - [Data](#data)
      - [**SetScreenVariable(name, value)**](#setscreenvariablename-value)
      - [**SetVariable(name, value)**](#setvariablename-value)
    - [Menu](#menu)
      - [**MainMenu(confirm=True)**](#mainmenuconfirmtrue)
      - [**Quit(confirm=None)**](#quitconfirmnone)
      - [**ShowMenu(screen=None)**](#showmenuscreennone)
      - [**Start(label=u'start')**](#startlabelustart)
    - [File](#file)
      - [**FileDelete(name, confirm=True, page=None, slot=False)**](#filedeletename-confirmtrue-pagenone-slotfalse)
      - [**FileLoad(name, confirm=True, page=None, newest=True, cycle=False, slot=False)**](#fileloadname-confirmtrue-pagenone-newesttrue-cyclefalse-slotfalse)
      - [**FilePage(page)**](#filepagepage)
      - [**FileSave(name, confirm=True, newest=True, page=None, cycle=False, slot=False)**](#filesavename-confirmtrue-newesttrue-pagenone-cyclefalse-slotfalse)
      - [**FileTakeScreenshot()**](#filetakescreenshot)
      - [**QuickLoad(confirm=True)**](#quickloadconfirmtrue)
      - [**QuickSave(message=u'Quick save complete.', newest=False)**](#quicksavemessageuquick-save-complete-newestfalse)
    - [Audio](#audio)
      - [**PauseAudio(channel, value=True)**](#pauseaudiochannel-valuetrue)
      - [**Play(channel, file, selected=None)**](#playchannel-file-selectednone)
      - [**Queue(channel, file)**](#queuechannel-file)
      - [**SetMixer(mixer, volume)**](#setmixermixer-volume)
      - [**SetMute(mixer, mute)**](#setmutemixer-mute)
      - [**Stop(channel)**](#stopchannel)
      - [**ToggleMute(mixer)**](#togglemutemixer)
    - [Other](#other)
      - [**Confirm(prompt, yes, no=None, confirm_selected=False)**](#confirmprompt-yes-nonone-confirm_selectedfalse)
      - [**Help(help=None)**](#helphelpnone)
      - [**If(expression, true=None, false=None)**](#ifexpression-truenone-falsenone)
      - [**Notify(message)**](#notifymessage)
      - [**RollForward()**](#rollforward)
      - [**Rollback()**](#rollback)
      - [**Screenshot()**](#screenshot)
      - [**Skip(fast=False, confirm=False)**](#skipfastfalse-confirmfalse)
  - [Control Statements](#control-statements)
    - [`default`](#default)
    - [`for`](#for)
    - [`if`](#if)
    - [`on`](#on)
    - [`use`](#use)
    - [`has`](#has)
    - [`showif`](#showif)
  - [Tooltips](#tooltips)
    - [`tooltip`](#tooltip)
    - [**GetTooltip(screen=None)**](#gettooltipscreennone)
  - [Reviewing Concepts](#reviewing-concepts)

---

## Actions

Many user interface keywords in Ren'Py accept *actions*. As part of the screen language, an *action* is any of a large number of methods defined to interact in different ways.

> An *action* is a function defined in Ren'Py for navigating screens, manipulating files, or otherwise changing values.

### Control

Functions that are part of showing, hiding, and navigating between screens are classified as *Control*.

#### **Call(label)**

Ends the current label and transfers control to another.

#### **Hide(screen, transition=None)**

Hides a currently shown screen with an optional transition.

#### **Jump(label)**

"Jumps" to a known label within the script.

#### **NullAction()**

Performs no action. It can be used as a default or other "action" to do nothing.

#### **Return(value=None)**

"Returns" data from a previously called label.

#### **Show(screen, transition=None)**

"Shows" a screen with an optional transition.

### Data

Functions that adjust data values are classified as *Data*.

#### **SetScreenVariable(name, value)**

Changes the *value* of a screen variable *name*.

#### **SetVariable(name, value)**

Changes the *value* of a variable *name*.

### Menu

Functions that work with the MainMenu are classified as *Menu*.

#### **MainMenu(confirm=True)**

Calls the MainMenu, prompting a confirmation. If *confirm* is `True`, no conformation will be created.

#### **Quit(confirm=None)**

Quits, prompting a confirmation. If *confirm* is `True`, no conformation will be created.

#### **ShowMenu(screen=None)**

Shows a known screen.

#### **Start(label=u'start')**

"Starts" the script at a label from a menu context. If no label is provided, it begins at the lable "start". Otherwise, it begins at the *label* specified.

### File

File functions work with two concepts:

- *name*: File to manipulate
- *page*: "auto", "quick", or an integer.

#### **FileDelete(name, confirm=True, page=None, slot=False)**

- *name*: The name of the slot to delete.

- *confirm*: If `True` and not at the main menu, prompt for confirmation before loading the file.

- *page*: The page that the file will be loaded from. If None, the current page is used.
slot. If `True`, name is taken to be a slot name, and page is ignored.

#### **FileLoad(name, confirm=True, page=None, newest=True, cycle=False, slot=False)**

- *name*: The name of the slot to load from. If None, an unused slot will be used, and hence the file will not be loadable.

- *confirm*: If true and not at the main menu, prompt for confirmation before loading the file.
page. The page that the file will be loaded from. If None, the current page is used.

- *newest*: If `True`, the button is selected if this is the newest file.

- *cycle*: Ignored.

- *slot*: If `True`, name is taken to be a slot name, and page is ignored.

#### **FilePage(page)**

Sets the file page to page, which should be one of "auto", "quick", or an integer.

#### **FileSave(name, confirm=True, newest=True, page=None, cycle=False, slot=False)**

- *name*: The name of the slot to save to. If None, an unused slot (a large number based on the current time) will be used.

- *confirm*: If `True`, then we will prompt before overwriting a file.

- *newest*: Ignored.

- *page*: The name of the page that the slot is on. If None, the current page is used.

- *cycle*: If `True`, then saves on the supplied page will be cycled before being shown to the user. `config.quicksave_slots` slots are used in the cycle.

- *slot*: If `True`, name is taken to be a slot name, and page is ignored.

#### **FileTakeScreenshot()**

Take a screenshot to be used when the game is saved.

#### **QuickLoad(confirm=True)**

- *confirm*: If `True` and not at the main menu, prompt for confirmation before loading the file.

#### **QuickSave(message=u'Quick save complete.', newest=False)**

- *message*: A message to display to the user when the quick save finishes.

- *newest*: Set to `True` to mark the quicksave as the newest save.

### Audio

#### **PauseAudio(channel, value=True)**

Sets the pause flag for channel. If *value* is `True`, the channel is paused. If `False`, the channel is unpaused. If "toggle", the pause flag will be toggled.

#### **Play(channel, file, selected=None)**

- *channel*: The channel to play the sound on.

- *file*: The file to play.

- *selected*: If `True`, buttons using this action will be marked as selected if the file is playing on the channel. If `False`, this action will not cause the button to start playing. If `None`, the button is marked selected if the channel is a music channel, and not otherwise.

#### **Queue(channel, file)**

- *channel*: The channel to play the sound on.

- *file*: The file to play.

#### **SetMixer(mixer, volume)**

- *mixer*: The mixer to set the volume of. A string, usually one of "music", "sfx", or "voice".

- *value*: The value to set the volume to. A number between 0.0 and 1.0, inclusive.

#### **SetMute(mixer, mute)**

- *mixer*: Either a single string giving a mixer name, or a list of strings giving a list of mixers. The strings should be mixer names, usually "music", "sfx", or "voice".

- *mute*: `True` to mute the mixer, `False` to ummute it.

#### **Stop(channel)**

- *channel*: The channel to stop the sound on.

#### **ToggleMute(mixer)**

- *mixer*: Either a single string giving a mixer name, or a list of strings giving a list of mixers. The strings should be mixer names, usually "music", "sfx", or "voice".

### Other

#### **Confirm(prompt, yes, no=None, confirm_selected=False)**

- *prompt*: The prompt to display to the user.

- *confirm_selected*: If `True`, the prompt will be displayed even if the yes action is already selected. If `False` (the default), the prompt will not be displayed if the yes action is selected.

#### **Help(help=None)**

- *help*: A string that is used to find help.

#### **If(expression, true=None, false=None)**

This returns `True` if expression is true, and `False` otherwise.

#### **Notify(message)**

Displays *message*.

#### **RollForward()**

This action causes a rollforward to occur, if a roll forward is possible.

#### **Rollback()**

This action causes a rollback to occur, when a rollback is possible.

#### **Screenshot()**

Takes a screenshot.

#### **Skip(fast=False, confirm=False)**

- *fast*: If `True`, skips directly to the next menu choice.

- *confirm*: If `True`, asks for confirmation before beginning skipping.

## Control Statements

A *control statement* "controls" the flow of other statements around it in a screen.

### `default`

Sets the default value of a variable within a screen. If no values are passed to the screen, `default` can be used to define it.

```Python
screen example():
    default club = None
```

### `for`

The `for` statement is similar to the Python `for` statement.

```Python
$ numerals = [ 'I', 'II', 'III', 'IV', 'V' ]

screen five_buttons():
    vbox:
        for i, numeral in enumerate(numerals):
            textbutton numeral action Return(i + 1)
```

### `if`

The screen language `if` statement is the same as the Python `if` statement.

```Python
screen skipping_indicator():
    if config.skipping:
         text "Skipping."
    else:
         text "Not Skipping."
```

### `on`

The `on` statement allows the screen to execute an action when an event occurs.

Options include:

- "show"
- "hide"
- "replace"
- "replaced"

### `use`

The `use` statement allows a screen to include another.

```Python
screen ed(num):
    text "Ed"
    text "Captain"

screen kelly(num):
    text "Kelly"
    text "First Officer"

screen bortus(num):
    text "Bortus"
    text "Second Officer"

screen crew():
    hbox:
        for i, member in enumerate(party):
            vbox:
                use expression member.screen pass (i + 1)
```

### `has`

Specifies a container to use, instead of `fixed`, for statements that take only one child.

The `has` statement can be supplied as a child of the following statements:

- `button`
- `frame`
- `window`

The `has` statement can be given the following statements as a container.

- `fixed`
- `grid`
- `hbox`
- `side`
- `vbox`

```Python
screen volume_controls():
     frame:
         has vbox

         bar value Preference("sound volume")
         bar value Preference("music volume")
         bar value Preference("voice volume")
```

### `showif`

The `showif` statement wraps its children in a displayable that manages the show and hide process.

`showif` delivers three events to its children:

- *appear*: Is delivered if the condition is `True` when the screen is first shown, to instantly show the child.

- *show*: Is delivered when the condition changes from `False` to `True`.

- *hide*: Is delivered when the condition changes from `True` to `False`.

## Tooltips

### `tooltip`

Assigns a tooltip to this displayable.

### **GetTooltip(screen=None)**

Returns the tooltip of the currently focused displayable, or `None` if no displayable is focused.

- *screen*: If not `None`, this should be the name or tag of a screen. If given, this function only returns the tooltip if the focused displayable is part of the screen.

Example:

```Python
screen tooltip_example():
    vbox:
        textbutton "North":
            action Return("n")
            tooltip "To meet a polar bear."

        textbutton "South":
            action Return("s")
            tooltip "All the way to the tropics."

        textbutton "East":
            action Return("e")
            tooltip "So we can embrace the dawn."

        textbutton "West":
            action Return("w")
            tooltip "Where to go to see the best sunsets."

        $ tooltip = GetTooltip()

        if tooltip:
            text "[tooltip]"
```

## Reviewing Concepts

An *Action* is one of many built-in functions in Ren'Py.

Actions are classified into different categories including Control, Data, File, and Audio.

A control statement (as part of the screen language in Ren'Py) "controls" the flow of statements within a screen. This includes the keywords `if` and `for`, both of which act like the Python keywords.
