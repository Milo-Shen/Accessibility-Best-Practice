# ComboBox

[Combobox](https://www.w3.org/TR/wai-aria-1.1/#combobox) is a widget made up of the combination of two distinct elements:   

1. A single-line textbox. 
2. An associated pop-up element for helping users set the value of the textbox. The popup may be a:
	1. [listbox](https://www.w3.org/TR/wai-aria-practices-1.1/#Listbox)
	2. [grid](https://www.w3.org/TR/wai-aria-practices-1.1/#grid)
	3. [tree](https://www.w3.org/TR/wai-aria-practices-1.1/#TreeView)
	4. [dialog](https://www.w3.org/TR/wai-aria-practices-1.1/#dialog_modal)   
3. Many implementations also include a third optional element -- a graphical button adjacent to the textbox, indicating the availability of the popup. Activating the button displays the popup if suggestions are available.

## Popup display conditions
The popup is hidden by default, and the conditions that trigger its display are specific to each implementation. Some possible popup display conditions include:

- It is displayed only if a certain number of characters are typed in the textbox and those characters match some portion of one of the suggested values.
- It is displayed as soon as the textbox is focused, even if the textbox is empty.
- It is displayed when the Down Arrow key is pressed or the show button is activated, possibly with a dependency on the content of the textbox.
- It is displayed if the value of the textbox is altered in a way that creates one or more partial matches to a suggested value.

## Usage scenarios
1. The value for the textbox must be chosen from a predefined set of allowed values, e.g., a location field must contain a valid location name. Note that the listbox and menu button patterns are also useful in this scenario; differences between combobox and alternative patterns are described below.
2. The textbox may contain any arbitrary value, but it is advantageous to suggest possible values to the user, e.g., a search field may suggest similar or previous searches to save the user time.

## Autocomplete behavior
The nature of the suggested values and the way the suggestions are presented is called the autocomplete behavior. Comboboxes can have one of four forms of autocomplete:

1. **No autocomplete:** When the popup is triggered, the suggested values it contains are the same regardless of the characters typed in the textbox. For example, the popup suggests a set of recently entered values, and the suggestions do not change as the user types.
2. **List autocomplete with manual selection:** When the popup is triggered, it presents suggested values that complete or logically correspond to the characters typed in the textbox. The character string the user has typed will become the value of the textbox unless the user selects a value in the popup.
3. **List autocomplete with automatic selection:** When the popup is triggered, it presents suggested values that complete or logically correspond to the characters typed in the textbox, and the first suggestion is automatically highlighted as selected. The automatically selected suggestion becomes the value of the textbox when the combobox loses focus unless the user chooses a different suggestion or changes the character string in the textbox.
4. **List with inline autocomplete:** This is the same as list with automatic selection with one additional feature. The portion of the selected suggestion that has not been typed by the user, a completion string, appears inline after the input cursor in the textbox. The inline completion string is visually highlighted and has a selected state.

## The difference between listbox and menu button
1. The value of the combobox is presented in an edit field
2.  In many implementations, users can navigate the set of allowed values in a combobox or menu and then decide to revert to the value the widget had before navigating by pressing escape. In contrast, navigating a listbox immediately changes its value, and escape does not provide an undo mechanism.

## Attention
1. Authors *MUST* ensure an element with role `combobox` contains or owns a text input element with role `textbox` or [`searchbox`](https://www.w3.org/TR/wai-aria-1.1/#searchbox) and that the text input has [`aria-multiline`](https://www.w3.org/TR/wai-aria-1.1/#aria-multiline) set to `false`. 
2. If the `combobox` provides autocompletion behavior for the text input as described in [`aria-autocomplete`](https://www.w3.org/TR/wai-aria-1.1/#aria-autocomplete), authors *MUST* set `aria-autocomplete` on the `textbox` element to the value that corresponds to the provided behavior.
3. The default state of a `combobox` is collapsed. In the collapsed state, only the `textbox` element of a `combobox` is visible. A `combobox` is said to be expanded when both the `textbox` and a secondary element that serves as its popup are visible. Authors *MUST* set [`aria-expanded`](https://www.w3.org/TR/wai-aria-1.1/#aria-expanded) to `true` on an element with role `combobox` when it is expanded and `false` when it is collapsed. Elements with the role `combobox` have an implicit `aria-expanded` value of `false`.
4. When a combobox is expanded, authors MUST ensure it contains or owns an element that has a role of listbox, tree, grid, or dialog. This element is the combobox popup. When the combobox is expanded, authors MUST set aria-controls on the textbox element to a value that refers to the combobox popup element.
5. Elements with the role `combobox` have an implicit [`aria-haspopup`](https://www.w3.org/TR/wai-aria-1.1/#aria-haspopup) value of `listbox`. If the `combobox` popup element has a role other than `listbox`, authors *MUST* specify a value for `aria-haspopup` that corresponds to the type of its popup.
6. To be [keyboard accessible](https://www.w3.org/TR/wai-aria-1.1/#dfn-keyboard-accessible), authors *SHOULD* manage focus of descendants for all instances of this [role](https://www.w3.org/TR/wai-aria-1.1/#dfn-role), as described in [Managing Focus](https://www.w3.org/TR/wai-aria-1.1/#managingfocus). <b>When a `combobox` receives focus, authors *SHOULD* ensure focus is placed on the `textbox` element.</b>
7. Authors *SHOULD* provide keyboard mechanisms for moving focus between the `textbox` element and the elements contained in the popup. For example, one common convention is that Down Arrow moves focus from the text input to the first focusable descendant of the popup element. If the popup element supports [`aria-activedescendant`](https://www.w3.org/TR/wai-aria-1.1/#aria-activedescendant), in lieu of moving focus, such keyboard mechanisms can control the value of `aria-activedescendant` on the `textbox` element. When a descendant of the popup element is active, authors *MAY* set `aria-activedescendant` on the `textbox` to a value that refers to the active element within the popup while focus remains on the `textbox` element.

## Characteristic

| Characteristic                   | Value                                                        |
| -------------------------------- | ------------------------------------------------------------ |
| Superclass Role:                 | [`select`](https://www.w3.org/TR/wai-aria-1.1/#select)       |
| Required Owned Elements:         | [`textbox`](https://www.w3.org/TR/wai-aria-1.1/#textbox) and, when expanded, one of:[`listbox`](https://www.w3.org/TR/wai-aria-1.1/#listbox)[`tree`](https://www.w3.org/TR/wai-aria-1.1/#tree)[`grid`](https://www.w3.org/TR/wai-aria-1.1/#grid)[`dialog`](https://www.w3.org/TR/wai-aria-1.1/#dialog) |
| Required States and Properties:  | [`aria-controls`](https://www.w3.org/TR/wai-aria-1.1/#aria-controls)<br/>[`aria-expanded`](https://www.w3.org/TR/wai-aria-1.1/#aria-expanded) |
| Supported States and Properties: | [`aria-autocomplete`](https://www.w3.org/TR/wai-aria-1.1/#aria-autocomplete)<br/>[`aria-readonly`](https://www.w3.org/TR/wai-aria-1.1/#aria-readonly)<br/>[`aria-required`](https://www.w3.org/TR/wai-aria-1.1/#aria-required) |
| Name From:                       | author                                                       |
| Accessible Name Required:        | True                                                         |
| Implicit Value for Role:         | Default for [`aria-expanded`](https://www.w3.org/TR/wai-aria-1.1/#aria-expanded) is `false`.<br/> Default for [`aria-haspopup`](https://www.w3.org/TR/wai-aria-1.1/#aria-haspopup) is `listbox`. |

## Keyboard Interaction

- Tab: The textbox is in the page Tab sequence.
- <b>Note: The popup indicator icon or button (if present), the popup, and the popup descendants are excluded from the page Tab sequence.</b>

## Textbox Keyboard Interaction
When focus is in the textbox:

- Down Arrow: If the popup is available, moves focus into the popup:
  - If the autocomplete behavior automatically selected a suggestion before Down Arrow was pressed, focus is placed on the suggestion following the automatically selected suggestion.
  - Otherwise, places focus on the first focusable element in the popup.
- Up Arrow (Optional): If the popup is available, places focus on the last focusable element in the popup.
- Escape: Dismisses the popup if it is visible. Optionally, clears the textbox.
- Enter: If an autocomplete suggestion is automatically selected, accepts the suggestion either by placing the input cursor at the end of the accepted value in the textbox or by performing a default action on the value. For example, in a messaging application, the default action may be to add the accepted value to a list of message recipients and then clear the textbox so the user can add another recipient.
- Printable Characters: Type characters in the textbox. Note that some implementations may regard certain characters as invalid and prevent their input.
- Standard single line text editing keys appropriate for the device platform (see note below).
- Alt + Down Arrow (Optional): If the popup is available but not displayed, displays the popup without moving focus.
- Alt + Up Arrow (Optional): If the popup is displayed:
  1. If the popup contains focus, returns focus to the textbox.
  2. Closes the popup.

### Standard single line text editing keys appropriate for the device platform:
1. include keys for input, cursor movement, selection, and text manipulation.
2. Standard key assignments for editing functions depend on the device operating system.
3. The most robust approach for providing text editing functions is to rely on browsers, which supply them for HTML inputs with type text and for elements with the `contenteditable` HTML attribute.
4. **IMPORTANT:** Be sure that JavaScript does not interfere with browser-provided text editing functions by capturing key events for the keys used to perform them.

## Basic Example

```
<div aria-label="Tag" role="combobox" aria-expanded="true" aria-owns="owned_listbox" aria-haspopup="listbox">
    <input type="text" aria-autocomplete="list" aria-controls="owned_listbox" aria-activedescendant="selected_option">
</div>
<ul role="listbox" id="owned_listbox">
    <li role="option">Zebra</li>
    <li role="option" id="selected_option">Zoom</li>
</ul>
```
