# Combobox with Listbox Popup
The belowing three examples demonstrates a different form of the autocomplete behaviors described in the [design pattern](https://www.w3.org/TR/wai-aria-practices-1.1/#combobox).

## Attention
1. <b> When the drop-down list pops up, the cursor is always on the input box </b>

## List Autocomplete with Manual Selection
### step

1. When the listbox popup is displayed, it contains suggested values that complete or logically correspond to the characters typed in the textbox. In this implementation, the values in the listbox have names that start with the characters typed in the textbox.
2. Users may set the value of the combobox by choosing a value from the list of suggested values.
3. If the user does not choose a value from the listbox before moving focus outside the combobox, the value that the user typed, if any, becomes the value of the combobox.

### html

```
<label for="ex1-input" id="ex1-label" class="combobox-label">
  Choice 1 Fruit or Vegetable
</label>
<div class="combobox-wrapper">
  <div
    role="combobox"
    aria-expanded="false"
    aria-owns="ex1-listbox"
    aria-haspopup="listbox"
    id="ex1-combobox"
  >
    <input
      type="text"
      aria-autocomplete="list"
      aria-controls="ex1-listbox"
      id="ex1-input"
    />
  </div>
  <ul
    aria-labelledby="ex1-label"
    role="listbox"
    id="ex1-listbox"
    class="listbox hidden"
  ></ul>
</div>
```

## List Autocomplete with Automatic Selection

### step

1. When the listbox popup is displayed, it contains suggested values that complete or logically correspond to the characters typed in the textbox. In this implementation, the values in the listbox have names that start with the characters typed in the textbox.
2. The first suggestion is automatically highlighted as selected.
3. The automatically selected suggestion becomes the value of the textbox when the combobox loses focus unless the user chooses a different suggestion or changes the character string in the textbox.

### html

```
<label id="ex2-label" class="combobox-label">
  Choice 2 Fruit or Vegetable
</label>
<div class="combobox-wrapper">
  <div
    role="combobox"
    aria-expanded="false"
    aria-owns="ex2-listbox"
    aria-haspopup="listbox"
    id="ex2-combobox"
  >
    <input
      type="text"
      aria-autocomplete="list"
      aria-controls="ex2-listbox"
      aria-labelledby="ex2-label"
      id="ex2-input"
    />
  </div>
  <ul
    aria-labelledby="ex2-label"
    role="listbox"
    id="ex2-listbox"
    class="listbox hidden"
  ></ul>
</div>
```

## List with Inline Autocomplete

### step

1. With the exception of one additional feature, this example has the same autocomplete behavior as the previous example that has list with automatic selection.
2. The additional feature is that the portion of the selected suggestion that has not been typed by the user, a completion string, appears inline after the input cursor in the textbox.
3. The inline completion string is visually highlighted and has a selected state.

### html

```
<label id="ex3-label" class="combobox-label">
      Choice 3 Fruit or Vegetable
</label>
<div class="combobox-wrapper">
  <div
    role="combobox"
    aria-expanded="false"
    aria-owns="ex3-listbox"
    aria-haspopup="listbox"
    id="ex3-combobox"
  >
    <input
      type="text"
      aria-autocomplete="both"
      aria-controls="ex3-listbox"
      aria-labelledby="ex3-label"
      id="ex3-input"
    />
    <div
      class="combobox-dropdown"
      id="ex3-combobox-arrow"
      tabindex="-1"
      role="button"
      aria-label="Show vegetable options"
    >
      <img src="imgs/arrow_drop_down_grey_27x27.png" alt="" />
    </div>
  </div>
  <ul
    aria-labelledby="ex3-label"
    role="listbox"
    id="ex3-listbox"
    class="listbox hidden"
  ></ul>
</div>
```

## Keyboard Support
### Textbox

| Key                                    | Function                                                     |
| -------------------------------------- | ------------------------------------------------------------ |
| Down Arrow                             | 1. If the listbox is displayed:<br/>&nbsp;&nbsp;Example 1: Moves focus to the first suggested value.<br/>&nbsp;&nbsp;Examples 2 and 3: Moves focus to the second suggested value. Note that the first value is automatically selected.<br/>2. If the listbox is not displayed, in example 3 only, opens the listbox and moves focus to the first value. |
| Up Arrow                               | 1. If the listbox is displayed, moves focus to the last suggested value.<br/>2. If the listbox is not displayed, in example 3 only, opens the listbox and moves focus to the last value. |
| Enter                                  | Example 1: Does nothing.<br/>Examples 2 and 3: If the listbox is displayed and the first option is automatically selected: <br/>&nbsp;&nbsp;1. Sets the textbox value to the content of the selected option.<br/>&nbsp;&nbsp;2. Closes the listbox. |
| Escape                                 | 1. Clears the textbox<br/>2. If the listbox is displayed, closes it. |
| Standard single line text editing keys | 1. Keys used for cursor movement and text manipulation, such as `Delete` and `Shift + Right` Arrow.<br/>2. An HTML `input` with `type=text` is used for the textbox so the browser will provide platform-specific editing keys |

### Listbox Popup
When visual focus is in the listbox, DOM focus remains on the textbox and the value of aria-activedescendant on the textbox is set to a value that refers to the listbox option that is visually indicated as focused. 

| Key                  | Function                                                     |
| -------------------- | ------------------------------------------------------------ |
| Enter                | 1. Sets the textbox value to the content of the focused option in the listbox.<br/>2. Closes the listbox.<br/>3. Sets focus on the textbox. |
| Escape               | 1. Closes the listbox.<br/>2. Sets focus on the textbox.<br/>3. Clears the textbox. |
| Down Arrow           | 1. Moves focus to the next option.<br/>2. If focus is on the last option, moves focus to the first option.<br/>3. Note: This wrapping behavior is useful when Home and End move the editing cursor as described below. |
| Up Arrow             | 1. Moves focus to the previous option.<br/>2. If focus is on the first option, moves focus to the last option.<br/>3. Note: This wrapping behavior is useful when Home and End move the editing cursor as described below. |
| Right Arrow          | Moves focus to the textbox and moves the editing cursor one character to the right. |
| Left Arrow           | Moves focus to the textbox and moves the editing cursor one character to the left. |
| Home                 | Moves focus to the textbox and places the editing cursor at the beginning of the field. |
| End                  | Moves focus to the textbox and places the editing cursor at the end of the field. |
| Printable Characters | Moves focus to the textbox.Types the character in the textbox. |

## Role, Property, State, and Tabindex Attributes

### Combobox Container

| Role       | Attribute               | Element | Usage                                                        |
| ---------- | ----------------------- | ------- | ------------------------------------------------------------ |
| `combobox` |                         | `div`   | 1. Identifies the element as a combobox.<br/>Note:<br>&nbsp;1. Unlike this ARIA 1.1 combobox, an ARIA 1.0 pattern would have the `combobox` role on the textbox input instead of a parent container of the textbox.<br/>&nbsp;2. The ARIA 1.1 pattern demonstrated on this page enables screen reader users to perceive both the input and the popup when using reading mode (see note below about aria-owns). |
|            | `aria-haspopup=listbox` | `div`   | 1. Indicates that the combobox can popup a `listbox` to suggest values.<br/>2. This is the default value for elements with the `combobox` role. |
|            | `aria-owns=IDREF`       | `div`   | 1. Refers to the element that serves as the listbox popup.<br/>2.<b>Tells browsers to arrange the screen reader reading order so the listbox, when it is visible, immediately follows the other elements inside the combobox, regardless of where the listbox element is in the DOM.</b>b> |
|            | `aria-expanded=false`   | `div`   | Indicates that the popup element **is not** displayed.       |
|            | `aria-expanded=true`    | `div`   | Indicates that the popup element **is** displayed.           |

### Textbox
| Role | Attribute                     | Element              | Usage                                                        |
| ---- | ----------------------------- | -------------------- | ------------------------------------------------------------ |
|      | `id="string"`                 | `input[type="text"]` | 1. Referenced by `for` attribute of `label` element to provide an accessible label.<br/>2. Recommended labeling method for HTML input elements so clicking label focuses input. |
|      | `aria-autocomplete=list`      | `input[type="text"]` | Examples 1 and 2: Indicates that the autocomplete behavior of the text input is to suggest a list of possible values in a popup and that the suggestions are related to the string that is present in the textbox. |
|      | `aria-autocomplete=both`      | `input[type="text"]` | Example 3: Indicates that the autocomplete behavior of the text input is to both show an inline completion string and suggest a list of possible values in a popup where the suggestions are related to the string that is present in the textbox. |
|      | `aria-controls=IDREF`         | `input[type="text"]` | 1. Identifies the popup element that lists suggested values.<br/>2. Note:<br/>&nbsp;1. In the ARIA 1.0 combobox pattern, the textbox has `aria-owns` instead of `aria-controls`.<br/>&nbsp;2. In this ARIA 1.1 pattern, `aria-owns` is instead on the parent container so the popup element is a sibling of the textbox instead of a child of the textbox, making it perceivable by screen reader users as an element adjacent to the textbox when using a reading cursor or touch interface. |
|      | `aria-activedescendant=IDREF` | `input[type="text"]` | 1. When an option in the listbox is visually indicated as having keyboard focus, refers to that option.<br/>2. When navigation keys, such as Down Arrow, are pressed, the JavaScript changes the value.<br/>3. Enables assistive technologies to know which element the application regards as focused while DOM focus remains on the `input` element.<br/>4. For more information about this focus management technique, see [Using aria-activedescendant to Manage Focus.](https://www.w3.org/TR/wai-aria-practices-1.1/#kbd_focus_activedescendant) |

### Listbox Popup

| Role      | Attribute               | Element | Usage                                                        |
| --------- | ----------------------- | ------- | ------------------------------------------------------------ |
| `listbox` |                         | `ul`    | Identifies the `ul` element as a `listbox`.                  |
|           | `aria-labelledby=IDREF` | `ul`    | Provides a label for the `listbox` element of the combobox.  |
| `option`  |                         | `li`    | 1. Identifies the element as a `listbox` `option`.<br/>2. The text content of the element provides the accessible name of the `option`. |
|           | `aria-selected=true`    | `li`    | 1. Specified on an option in the listbox when it is visually highlighted as selected.<br/>2. In example 1, occurs only when an option in the list is referenced by `aria-activedescendant`.<br/>3. In examples 2 and 3, also occurs when focus is in the textbox and the first option is automatically selected. |
