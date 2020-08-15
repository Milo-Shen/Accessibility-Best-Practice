# [Legacy] Combobox With Both List and Inline Autocomplete ( aria 1.0 )

This example illustrates the autocomplete behavior referred to in the pattern as list with inline completion.

## step
1.  If the user types one or more characters in the edit box and the typed characters match the beginning of the name of one or more states or territories, a listbox popup appears containing the matching names, and the first match is automatically selected.
2. The portion of the selected suggestion that has not been typed by the user, a completion string, appears inline after the input cursor in the textbox
3. The automatically selected suggestion becomes the value of the textbox when the combobox loses focus unless the user chooses a different suggestion or changes the character string in the textbox.
4. The implementation  does not prevent input of any other arbitrary value.

## Keyboard Support
### Textbox

| Key                                    | Function                                                     |
| -------------------------------------- | ------------------------------------------------------------ |
| Down Arrow                             | 1. If the listbox is displayed and a suggestion is selected, moves visual focus to the next suggested value.<br/>2. If the textbox is empty and the listbox is not displayed, opens the listbox and moves visual focus to the first option. <br/>3. <b>In both cases DOM focus remains on the textbox.</b> |
| Up Arrow                               | 1. If the listbox is displayed and a suggestion is selected, moves visual focus to the last suggested value.<br/>2. If the textbox is empty, first opens the listbox if it is not already displayed and then moves visual focus to the last option.<br/>3.<b> In both cases DOM focus remains on the textbox.</b> |
| Enter                                  | 1. Sets the textbox value to the content of the selected option.<br/>2. Closes the listbox. |
| Escape                                 | 1. Clears the textbox.<br/>2. If the listbox is displayed, closes it. |
| Standard single line text editing keys | 1. Keys used for cursor movement and text manipulation, such as Delete and Shift + Right Arrow.<br/>2. An HTML `input` with `type="text"` is used for the textbox so the browser will provide platform-specific editing keys. |

### Listbox Popup

**NOTE:** When visual focus is in the listbox, DOM focus remains on the textbox and the value of `aria-activedescendant` on the textbox is set to a value that refers to the listbox option that is visually indicated as focused. 

| Key                  | Function                                                     |
| -------------------- | ------------------------------------------------------------ |
| Enter                | 1. Sets the textbox value to the content of the focused option in the listbox.<br/>2. Closes the listbox.<br/>3. Sets visual focus on the textbox. |
| Escape               | 1. Clears the textbox.<br/>2. Closes the listbox.<br/>3. Sets visual focus on the textbox. |
| Down Arrow           | 1. Moves visual focus to the next option.<br/>2. If visual focus is on the last option, moves visual focus to the first option.<br/>Note: This wrapping behavior is useful when `Home` and `End` move the editing cursor as described below. |
| Up Arrow             | 1. Moves visual focus to the previous option.<br/>2. If visual focus is on the first option, moves visual focus to the last option.<br/>3. Note: This wrapping behavior is useful when Home and End move the editing cursor as described below. |
| Right Arrow          | Moves visual focus to the textbox and moves the editing cursor one character to the right. |
| Left Arrow           | Moves visual focus to the textbox and moves the editing cursor one character to the left. |
| Home                 | Moves visual focus to the textbox and places the editing cursor at the beginning of the field. |
| End                  | Moves visual focus to the textbox and places the editing cursor at the end of the field. |
| Printable Characters | 1. Moves visual focus to the textbox.<br/>2. Types the character in the textbox. |

## Role, Property, State, and Tabindex Attributes

### Textbox

| Role       | Attribute                       | Element              | Usage                                                        |
| ---------- | ------------------------------- | -------------------- | ------------------------------------------------------------ |
| `combobox` |                                 | `input[type="text"]` | Identifies the input as a combobox.<br>Note: The primary difference between the ARIA 1.0 pattern and the ARIA 1.1 pattern is the placement of the `combobox` role. |
|            | `aria-autocomplete="both"`      | `input[type="text"]` | Indicates that the autocomplete behavior of the text input is to both show an inline completion string and suggest a list of possible values in a popup where the suggestions are related to the string that is present in the textbox. |
|            | `aria-haspopup="true"`          | `input[type="text"]` | Indicates that the combobox can popup another element to suggest values. |
|            | `aria-owns="#IDREF"`            | `input[type="text"]` | Identifies the element that serves as the popup.<br/>Note: In the ARIA 1.1 combobox pattern, the combobox uses `aria-controls` instead of `aria-owns`. |
|            | `aria-expanded="false"`         | `input[type="text"]` | Indicates that the popup element **is not** displayed.       |
|            | `aria-expanded="true"`          | `input[type="text"]` | Indicates that the popup element **is** displayed.           |
|            | `aria-activedescendant="IDREF"` | `input[type="text"]` | When an option in the listbox is visually indicated as having keyboard focus, refers to that option.<br/>When navigation keys, such as Down Arrow, are pressed, the JavaScript changes the value.<br/>Enables assistive technologies to know which element the application regards as focused while DOM focus remains on the `input` element.<br/>For more information about this focus management technique, see [Using aria-activedescendant to Manage Focus.](https://www.w3.org/TR/wai-aria-practices-1.1/#kbd_focus_activedescendant) |

### Listbox Popup

| Role      | Attribute              | Element | Usage                                                        |
| --------- | ---------------------- | ------- | ------------------------------------------------------------ |
| `listbox` |                        | `ul`    | Identifies the `ul` element as a `listbox`.                  |
|           | `aria-label="States"`  | `ul`    | Provides a label for the `listbox`.                          |
| `option`  |                        | `li`    | 1. Identifies the element as a `listbox` `option`.<br/>2. The text content of the element provides the accessible name of the `option`. |
|           | `aria-selected="true"` | `li`    | 1. Specified on an option in the listbox when it is visually highlighted as selected.<br/>2. Occurs when an option in the list is referenced by `aria-activedescendant` and when focus is in the textbox and the first option is automatically selected. |

## Basic Example - HTML

```
<div class="combobox-list">
  <label for="cb1-input">State</label>
  <div class="group">
    <input
      id="cb1-input"
      class="cb_edit"
      type="text"
      role="combobox"
      aria-autocomplete="both"
      aria-expanded="false"
      aria-haspopup="true"
      aria-owns="lb1"
    />
    <button id="cb1-button" aria-label="Open" tabindex="-1">&#9661;</button>
  </div>
  <ul id="lb1" role="listbox" aria-label="States">
    <li id="lb1-al" role="option">Alabama</li>
    <li id="lb1-ak" role="option">Alaska</li>
    <li id="lb1-as" role="option">American Samoa</li>
    <li id="lb1-az" role="option">Arizona</li>
    <li id="lb1-ar" role="option">Arkansas</li>
    <li id="lb1-ca" role="option">California</li>
    <li id="lb1-co" role="option">Colorado</li>
    <li id="lb1-ct" role="option">Connecticut</li>
    <li id="lb1-de" role="option">Delaware</li>
    <li id="lb1-dc" role="option">District of Columbia</li>
    <li id="lb1-fl" role="option">Florida</li>
    <li id="lb1-ga" role="option">Georgia</li>
    <li id="lb1-gm" role="option">Guam</li>
    <li id="lb1-hi" role="option">Hawaii</li>
    <li id="lb1-id" role="option">Idaho</li>
    <li id="lb1-il" role="option">Illinois</li>
    <li id="lb1-in" role="option">Indiana</li>
    <li id="lb1-ia" role="option">Iowa</li>
    <li id="lb1-ks" role="option">Kansas</li>
    <li id="lb1-ky" role="option">Kentucky</li>
    <li id="lb1-la" role="option">Louisiana</li>
    <li id="lb1-me" role="option">Maine</li>
    <li id="lb1-md" role="option">Maryland</li>
    <li id="lb1-ma" role="option">Massachusetts</li>
    <li id="lb1-mi" role="option">Michigan</li>
    <li id="lb1-mn" role="option">Minnesota</li>
    <li id="lb1-ms" role="option">Mississippi</li>
    <li id="lb1-mo" role="option">Missouri</li>
    <li id="lb1-mt" role="option">Montana</li>
    <li id="lb1-ne" role="option">Nebraska</li>
    <li id="lb1-nv" role="option">Nevada</li>
    <li id="lb1-nh" role="option">New Hampshire</li>
    <li id="lb1-nj" role="option">New Jersey</li>
    <li id="lb1-nm" role="option">New Mexico</li>
    <li id="lb1-ny" role="option">New York</li>
    <li id="lb1-nc" role="option">North Carolina</li>
    <li id="lb1-nd" role="option">North Dakota</li>
    <li id="lb1-mp" role="option">Northern Marianas Islands</li>
    <li id="lb1-oh" role="option">Ohio</li>
    <li id="lb1-ok" role="option">Oklahoma</li>
    <li id="lb1-or" role="option">Oregon</li>
    <li id="lb1-pa" role="option">Pennsylvania</li>
    <li id="lb1-pr" role="option">Puerto Rico</li>
    <li id="lb1-ri" role="option">Rhode Island</li>
    <li id="lb1-sc" role="option">South Carolina</li>
    <li id="lb1-sd" role="option">South Dakota</li>
    <li id="lb1-tn" role="option">Tennessee</li>
    <li id="lb1-tx" role="option">Texas</li>
    <li id="lb1-ut" role="option">Utah</li>
    <li id="lb1-ve" role="option">Vermont</li>
    <li id="lb1-va" role="option">Virginia</li>
    <li id="lb1-vi" role="option">Virgin Islands</li>
    <li id="lb1-wa" role="option">Washington</li>
    <li id="lb1-wv" role="option">West Virginia</li>
    <li id="lb1-wi" role="option">Wisconsin</li>
    <li id="lb1-wy" role="option">Wyoming</li>
  </ul>
</div>
```