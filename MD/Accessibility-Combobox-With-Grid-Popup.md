# Combobox with Grid Popup

## Keyboard Support
When visual focus is in the grid, DOM focus remains on the textbox and the value of `aria-activedescendant` on the textbox is set to a value that refers to an element in the grid that is visually indicated as focused.

### Textbox

| Key                                    | Function                                                     |
| -------------------------------------- | ------------------------------------------------------------ |
| Down Arrow                             | If the grid is displayed, moves focus to the first suggested value. |
| Up Arrow                               | If the grid is displayed, moves focus to the last suggested value. |
| Escape                                 | 1. Clears the textbox<br/>2. If the grid is displayed, closes it. |
| Standard single line text editing keys | 1. Keys used for cursor movement and text manipulation, such as Delete and Shift + Right Arrow.<br/>2. An HTML `input` with `type=text` is used for the textbox so the browser will provide platform-specific editing keys. |

### Grid Popup

| Key                  | Function                                                     |
| -------------------- | ------------------------------------------------------------ |
| Enter                | 1. Sets the textbox value to the content of the first cell in the row containing focus.<br>2. Closes the grid popup.<br/>3. Sets focus on the textbox. |
| Escape               | 1. Closes the grid popup.<br/>2. Sets focus on the textbox.<br/>3. Clears the textbox. |
| Down Arrow           | 1. Moves focus to the next row.If focus is in the last row, moves focus to the first row.<br/>Note: This wrapping behavior is useful when Home and End move the editing cursor as described below. |
| Up Arrow             | 1. Moves focus to the previous row.<br/>2. If focus is in the first row, moves focus to the last row.<br/>Note: This wrapping behavior is useful when Home and End move the editing cursor as described below. |
| Right Arrow          | 1. Moves focus to the next cell.<br/>2. If focus is in the last cell in a row, moves focus to the first cell in the next row. <br/>3. If focus is in the last cell in the last row, moves focus to the first cell in the first row. |
| Left Arrow           | 1. Moves focus to the previous cell.<br/>2. If focus is in the first cell in a row, moves focus to the last cell in the previous row.<br/>3. If focus is in the first cell in the first row, moves focus to the last cell in the last row. |
| Home                 | Moves focus to the textbox and places the editing cursor at the beginning of the field. |
| End                  | Moves focus to the textbox and places the editing cursor at the end of the field. |
| Printable Characters | 1. Moves focus to the textbox.<br/>2. Types the character in the textbox. |

## Role, Property, State, and Tabindex Attributes
### Combobox Container

| Role       | Attribute             | Element | Usage                                                        |
| ---------- | --------------------- | ------- | ------------------------------------------------------------ |
| `combobox` |                       | `div`   | 1. Identifies the element as a combobox.<br/>Note:<br/>1. Unlike this ARIA 1.1 combobox, an ARIA 1.0 pattern would have the `combobox` role on the textbox input instead of a parent container of the textbox.<br/>2. The ARIA 1.1 pattern demonstrated on this page enables screen reader users to perceive both the input and the popup when using reading mode (see note below about aria-owns). |
|            | `aria-haspopup=grid`  | `div`   | Indicates that the combobox can popup a `grid` to suggest values. |
|            | `aria-owns=IDREF`     | `div`   | 1. Refers to the element that serves as the grid popup.<br/>2. Tells browsers to arrange the screen reader reading order so the grid, when it is visible, immediately follows the other elements inside the combobox, regardless of where the grid element is in the DOM. |
|            | `aria-expanded=false` | `div`   | Indicates that the popup element **is not** displayed.       |
|            | `aria-expanded=true`  | `div`   | Indicates that the popup element **is** displayed.           |

### Textbox

| Role | Attribute                     | Element              | Usage                                                        |
| ---- | ----------------------------- | -------------------- | ------------------------------------------------------------ |
|      | `id="string"`                 | `input[type="text"]` | 1. Referenced by `for` attribute of `label` element to provide an accessible label.<br/>2. Recommended labeling method for HTML input elements so clicking label focuses input. |
|      | `aria-autocomplete=list`      | `input[type="text"]` | Indicates that the autocomplete behavior of the text input is to suggest a list of possible values in a popup. |
|      | `aria-controls=IDREF`         | `input[type="text"]` | 1. Identifies the popup element that lists suggested values.<br/>Note:<br/>1. In the ARIA 1.0 combobox pattern, the textbox has `aria-owns` instead of `aria-controls`.<br/>2. In this ARIA 1.1 pattern, `aria-owns` is instead on the parent container so the popup element is a sibling of the textbox instead of a child of the textbox, making it perceivable by screen reader users as an element adjacent to the textbox when using a reading cursor or touch interface. |
|      | `aria-activedescendant=IDREF` | `input[type="text"]` | 1. When a cell in the grid is visually indicated as having keyboard focus, refers to that cell.<br/>2. When navigation keys, such as Down Arrow, are pressed, the JavaScript changes the value.<br/>3. Enables assistive technologies to know which element the application regards as focused while DOM focus remains on the `input` element.<br/>4. For more information about this focus management technique, see [Using aria-activedescendant to Manage Focus.](https://www.w3.org/TR/wai-aria-practices-1.1/#kbd_focus_activedescendant) |

### Grid Popup

| Role       | Attribute               | Element | Usage                                                        |
| ---------- | ----------------------- | ------- | ------------------------------------------------------------ |
| `grid`     |                         | `div`   | Identifies the element as a `grid`.                          |
|            | `aria-labelledby=IDREF` | `div`   | Provides a label for the `grid` element of the combobox.     |
| `row`      |                         | `div`   | Identifies the element containing all the cells for a row.   |
|            | `aria-selected=true`    | `div`   | 1. Specified on a row in the grid when it is visually indicated as selected.<br/>2. Occurs only when a cell in the grid is referenced by `aria-activedescendant`. |
| `gridcell` |                         | `div`   | Identifies the element containing the content for a single cell. |


