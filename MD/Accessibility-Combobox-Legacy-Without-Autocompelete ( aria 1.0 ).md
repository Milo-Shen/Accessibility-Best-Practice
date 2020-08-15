# [Legacy] Combobox without Autocomplete ( aria 1.0 )
This example illustrates the autocomplete behavior known as no autocomplete. The terms that appear in the listbox popup are not related to the string that is present in the textbox. In this implementation, The listbox popup is not automatically triggered; it is displayed only when the user opens it.

## Keyboard Support

### Textbox

| Key                                    | Function                                                     |
| -------------------------------------- | ------------------------------------------------------------ |
| Down Arrow                             | 1. First opens the listbox if it is not already displayed and then moves visual focus to the first option.<br/><b>2. DOM focus remains on the textbox.</b> |
| Up Arrow                               | 1. First opens the listbox if it is not already displayed and then moves visual focus to the last option.<br/><b>2. DOM focus remains on the textbox.</b> |
| Enter                                  | 1. Sets the textbox value to the content of the selected option.<br/>2. Closes the listbox if it is displayed. |
| Standard single line text editing keys | 1. Keys used for cursor movement and text manipulation, such as Delete and Shift + Right Arrow.<br/>2. An HTML `input` with `type="text"` is used for the textbox so the browser will provide platform-specific editing keys. |

### Listbox Popup

**NOTE:** When visual focus is in the listbox, DOM focus remains on the textbox and the value of `aria-activedescendant` on the textbox is set to a value that refers to the listbox option that is visually indicated as focused.

| Key                  | Function                                                     |
| -------------------- | ------------------------------------------------------------ |
| Enter                | Sets the textbox value to the content of the focused option in the listbox.Closes the listbox.Sets visual focus on the textbox. |
| Escape               | Clears the textbox.Closes the listbox.Sets visual focus on the textbox. |
| Down Arrow           | Moves visual focus to the next option.If visual focus is on the last option, moves visual focus to the first option.Note: This wrapping behavior is useful when Home and End move the editing cursor as described below. |
| Up Arrow             | Moves visual focus to the previous option.If visual focus is on the first option, moves visual focus to the last option.Note: This wrapping behavior is useful when Home and End move the editing cursor as described below. |
| Right Arrow          | Moves visual focus to the textbox and moves the editing cursor one character to the right. |
| Left Arrow           | Moves visual focus to the textbox and moves the editing cursor one character to the left. |
| Home                 | Moves visual focus to the textbox and places the editing cursor at the beginning of the field. |
| End                  | Moves visual focus to the textbox and places the editing cursor at the end of the field. |
| Printable Characters | Moves visual focus to the textbox.Types the character in the textbox. |

## Role, Property, State, and Tabindex Attributes

### Textbox

| Role       | Attribute                       | Element              | Usage                                                        |
| ---------- | ------------------------------- | -------------------- | ------------------------------------------------------------ |
| `combobox` |                                 | `input[type="text"]` | Identifies the input as a combobox.<br/>Note: The primary difference between the ARIA 1.0 pattern and the ARIA 1.1 pattern is the placement of the `combobox` role. |
|            | `aria-autocomplete="none"`      | `input[type="text"]` | Indicates that the suggestions in the combobox popup are not values that complete the current textbox input. |
|            | `aria-haspopup="true"`          | `input[type="text"]` | Indicates that the combobox can popup another element to suggest values. |
|            | `aria-owns="#IDREF"`            | `input[type="text"]` | Identifies the element that serves as the popup.<br/>Note: In the ARIA 1.1 combobox pattern, the combobox uses `aria-controls` instead of `aria-owns`. |
|            | `aria-expanded="false"`         | `input[type="text"]` | Indicates that the popup element **is not** displayed.       |
|            | `aria-expanded="true"`          | `input[type="text"]` | Indicates that the popup element **is** displayed.           |
|            | `aria-activedescendant="IDREF"` | `input[type="text"]` | 1. When an option in the listbox is visually indicated as having keyboard focus, refers to that option.<br/>2. When navigation keys, such as Down Arrow, are pressed, the JavaScript changes the value.<br/>3. Enables assistive technologies to know which element the application regards as focused while DOM focus remains on the `input` element.<br/>4. For more information about this focus management technique, see [Using aria-activedescendant to Manage Focus.](https://www.w3.org/TR/wai-aria-practices-1.1/#kbd_focus_activedescendant) |

### Listbox Popup

| Role      | Attribute                        | Element | Usage                                                        |
| --------- | -------------------------------- | ------- | ------------------------------------------------------------ |
| `listbox` |                                  | `ul`    | Identifies the `ul` element as a `listbox`.                  |
|           | `aria-label="Previous Searches"` | `ul`    | Provides a label for the `listbox`.                          |
| `option`  |                                  | `li`    | 1. Identifies the element as a `listbox` `option`.<br/>2. The text content of the element provides the accessible name of the `option`. |
|           | `aria-selected="true"`           | `li`    | 1. Specified on an option in the listbox when it is visually highlighted as selected.<br/>2. Occurs only when an option in the list is referenced by `aria-activedescendant`. |

## Basic Example - HTML

```
<div class="combobox-list">
  <label for="cb1-input">Search</label>
  <div class="group">
    <input
      id="cb1-input"
      class="cb_edit"
      type="text"
      role="combobox"
      aria-autocomplete="none"
      aria-expanded="false"
      aria-haspopup="true"
      aria-owns="cb1-listbox"
    />
    <button id="cb1-button" tabindex="-1" aria-label="Open">
      &#9661;
    </button>
  </div>
  <ul id="cb1-listbox" role="listbox" aria-label="Previous Searches">
    <li id="lb1-01" role="option">weather</li>
    <li id="lb1-02" role="option">salsa recipes</li>
    <li id="lb1-03" role="option">cheap flights to NY</li>
    <li id="lb1-04" role="option">dictionary</li>
    <li id="lb1-05" role="option">baseball scores</li>
    <li id="lb1-06" role="option">hotels in NY</li>
    <li id="lb1-07" role="option">mortgage calculator</li>
    <li id="lb1-08" role="option">restaurants near me</li>
    <li id="lb1-09" role="option">free games</li>
    <li id="lb1-10" role="option">gas prices</li>
    <li id="lb1-11" role="option">classical music</li>
  </ul>
</div>
```