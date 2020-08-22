# Date Picker Dialog
The example below includes a date input field and a button that opens a date picker that implements the [dialog design pattern](https://www.w3.org/TR/wai-aria-practices-1.1/#dialog-modal). The dialog contains a calendar that uses the [grid pattern](https://www.w3.org/TR/wai-aria-practices-1.1/#grid) to present buttons that enable the user to choose a day from the calendar. Choosing a date from the calendar closes the dialog and populates the date input field. When the dialog is opened, if the input field is empty, or does not contain a valid date, then the current date is focused in the calendar. Otherwise, the focus is placed on the day in the calendar that matches the value of the date input field.

## Accessibility Features

- When a date is chosen, the accessible name of the Choose Date button is updated to include the selected date. So, when the dialog closes and focus returns to the Choose Date button, screen reader users hear confirmation of the selected date in the button name.
- When the month or year of the calendar grid changes as users navigate the calendar or activate the buttons for next or previous month or year, a live region enables screen readers to announce the new month and year.
- The calendar grid provides hotkeys for changing the year and month as well as support for normal grid navigation keys.
- When the dialog opens and a date in the calendar grid receives focus, a live region enables screen readers to announce keyboard instructions for navigating the calendar grid. The instructions are also visible at the bottom of the dialog box.

## Keyboard Support

### Choose Date Button

| Key          | Function                                                     |
| ------------ | ------------------------------------------------------------ |
| Space, Enter | 1. Open the date picker dialog.<br/>2. Move focus to selected date, i.e., the date displayed in the date input text field. If no date has been selected, places focus on the current date. |

### Date Picker Dialog

| Key         | Function                                                     |
| ----------- | ------------------------------------------------------------ |
| ESC         | Closes the dialog and returns focus to the Choose Date button. |
| Tab         | 1. Moves focus to next element in the dialog Tab sequence.<br/>2. Note that, as specified in the [grid design pattern](https://www.w3.org/TR/wai-aria-practices-1.1/#grid), only one button in the calendar grid is in the Tab sequence.<br/>3. If focus is on the last button (i.e., OK), moves focus to the first button (i.e. Previous Year). |
| Shift + Tab | 1. Moves focus to previous element in the dialog Tab sequence.<br/>2. Note that, as specified in the [grid design pattern](https://www.w3.org/TR/wai-aria-practices-1.1/#grid), only one button in the calendar grid is in the Tab sequence.<br/>3. If focus is on the first button (i.e., Previous Year), moves focus to the last button (i.e. OK). |

### Date Picker Dialog: Month/Year Buttons

| Key          | Function                                                     |
| ------------ | ------------------------------------------------------------ |
| Space, Enter | Change the month and/or year displayed in the calendar grid. |

### Date Picker Dialog: Date Grid

| Key               | Function                                                     |
| ----------------- | ------------------------------------------------------------ |
| Space, Enter      | 1. Select the date, close the dialog, and move focus to the Choose Date button. <br/>2. Update the value of the Date input with the selected date.<br/>3. Update the accessible name of the Choose Date button to include the selected date. |
| Up Arrow          | Moves focus to the same day of the previous week.            |
| Down Arrow        | Moves focus to the same day of the next week.                |
| Right Arrow       | Moves focus to the next day.                                 |
| Left Arrow        | Moves focus to the previous day.                             |
| Home              | Moves focus to the first day (e.g Sunday) of the current week. |
| End               | Moves focus to the last day (e.g. Saturday) of the current week. |
| Page Up           | 1. Changes the grid of dates to the previous month.<br/>2. Sets focus on the same day of the same week. <br/>3. If that day does not exist, then moves focus to the same day of the previous or next week. |
| Shift + Page Up   | 1. Changes the grid of dates to the previous Year.<br/>2. Sets focus on the same day of the same week.<br/>3. If that day does not exist, then moves focus to the same day of the previous or next week. |
| Page Down         | 1. Changes the grid of dates to the next month.<br/>2. Sets focus on the same day of the same week. <br/>3. If that day does not exist, then moves focus to the same day of the previous or next week. |
| Shift + Page Down | 1. Changes the grid of dates to the next Year.<br/>2. Sets focus on the same day of the same week. <br/>3. If that day does not exist, then moves focus to the same day of the previous or next week. |

### Date Picker Dialog: OK and Cancel Buttons

| Key          | Function                                                     |
| ------------ | ------------------------------------------------------------ |
| Space, Enter | Activates the button:<br/>1. Cancel: Closes the dialog, moves focus to Choose Date button, does not update date in date input.<br/>2. OK: Closes the dialog, moves focus to Choose Date button, updates date in date input. |

## Role, Property, State, and Tabindex Attributes

### Choose Date Button

| Role | Attribute             | Element  | Usage                                                        |
| ---- | --------------------- | -------- | ------------------------------------------------------------ |
|      | `aria-label="String"` | `button` | The initial value of accessible name is Choose Date.When users select a date, the accessible name is updated to also include the selected date. |

### Date Picker Dialog

| Role     | Attribute                 | Element | Usage                                                        |
| -------- | ------------------------- | ------- | ------------------------------------------------------------ |
| `dialog` |                           | `div`   | Identifies the element as a dialog .                         |
|          | `aria-modal="true"`       | `div`   | Indicates the dialog is modal.                               |
|          | `aria-labelledby="IDREF"` | `div`   | Refers to the heading containing the currently displayed month and year, which defines the accessible name for the dialog. |
|          | `aria-live="polite"`      | `div`   | 1. Indicates the element that displays information about keyboard commands for navigating the grid should be automatically announced by screen readers.<br/>2. The script slightly delays display of the information so screen readers are more likely to read it after information related to change of focus. |

### Date Picker Dialog: Calendar Navigation Buttons

| Role | Attribute             | Element  | Usage                                                        |
| ---- | --------------------- | -------- | ------------------------------------------------------------ |
|      | `aria-label="String"` | `button` | Defines the accessible name of the button (e.g. Next Year).  |
|      | `aria-live="polite"`  | `h2`     | 1. When the month and/or year changes the content of the `h2` element is updated.<br/>2. Indicates the `h2` should be automatically announced by screen readers. |

### Date Picker Dialog: Date Grid

| Role   | Attribute               | Element  | Usage                                                        |
| ------ | ----------------------- | -------- | ------------------------------------------------------------ |
| `grid` |                         | `table`  | 1. Identifies the `table` element as a `grid` widget.<br/>2. Since the `grid` role is applied to a `table` element, the `row`, `colheader`, and `gridcell` roles do not need to be specified because they are implied by `tr`, `th`, and `td` tags. |
|        | `aria-labelledby=IDREF` | `table`  | Defines the accessible name for the `grid` using the `h2` that shows the month and year of the dates displayed in the grid. |
|        | `tabindex="0"`          | `button` | 1. Makes the button focusable and includes it in the dialog Tab sequence.<br/>2. Set dynamically by the JavaScript when the element is to be included in the dialog Tab sequence.<br/>3. At any given time, only one button within the grid is in the dialog Tab sequence.<br/>4. This approach to managing focus is described in the section on [roving tabindex](https://www.w3.org/TR/wai-aria-practices-1.1/#kbd_roving_tabindex). |
|        | `tabindex="-1"`         | `button` | 1. Makes the button focusable and excludes it from the dialog Tab sequence.<br/>2. Changed dynamically to `0` by the JavaScript when the button is to be included in the dialog Tab sequence.<br/>3. At any given time, only one button within the grid is in the dialog Tab sequence.<br/>4. This approach to managing focus is described in the section on [roving tabindex](https://www.w3.org/TR/wai-aria-practices-1.1/#kbd_roving_tabindex). |
|        | `aria-selected="true"`  | `button` | 1. Identifies the button for the currently selected date, i.e., the date value present in the date input.<br/>2. Only set on the button representing the currently selected date, no other buttons have `aria-selected` specified. |

**Note:** Since the names of the days of the week in the column headers are abbreviated to two characters, they may be difficult to understand when announced by a screen reader. An alternative column header name can be provided to screen readers by applying the `abbr` attribute to the `th` elements. So, each `th` element includes a `abbr` attribute containing the full spelling of the name of the day for that column.