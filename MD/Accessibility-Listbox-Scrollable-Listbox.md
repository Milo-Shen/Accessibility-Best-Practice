# Listboxes with Rearrangeable Options

The following example implementation of the [design pattern for listbox](https://www.w3.org/TR/wai-aria-practices-1.1/#Listbox) demonstrates a scrollable single-select listbox widget. This widget is functionally similar to an HTML `select` input where the `size` attribute has a value greater than one.

## Notes

This listbox is scrollable; it has more options than its height can accommodate.

1. Scrolling only works as expected if the listbox is the options' `offsetParent`. The example uses `position: relative` on the listbox to that effect.
2. When an option is focused that isn't (fully) visible, the listbox's scroll position is updated:
   1. If Up Arrow or Down Arrow is pressed, the previous or next option is scrolled into view.
   2. If Home or End is pressed, the listbox scrolls all the way to the top or to the bottom.
   3. If `focusItem` is called, the focused option will be scrolled to the top of the view if it was located above it or to the bottom if it was below it.
   4. If the mouse is clicked on a partially visible option, it will be scrolled fully into view.
3. When a fully visible option is focused in any way, no scrolling occurs.
4. Normal scrolling through any scrolling mechanism (including Page Up and Page Down) works as expected. The scroll position will jump as described for `focusItem` if a means other than a mouse click is used to change focus after scrolling.

## Keyboard Support

The example listboxes on this page implement the following keyboard interface. Other variations and options for the keyboard interface are described in the [Keyboard Interaction section of the Listbox Design Pattern.](https://www.w3.org/TR/wai-aria-practices-1.1/#listbox_kbd_interaction)

| Key        | Function                                        |
| ---------- | ----------------------------------------------- |
| Down Arrow | Moves focus to and selects the next option.     |
| Up Arrow   | Moves focus to and selects the previous option. |
| Home       | Moves focus to and selects the first option.    |
| End        | Moves focus to and selects the last option.     |

## Role, Property, State, and Tabindex Attributes

The example listboxes on this page implement the following ARIA roles, states, and properties. Information about other ways of applying ARIA roles, states, and properties is available in the [Roles, States, and Properties section of the Listbox Design Pattern.](https://www.w3.org/TR/wai-aria-practices-1.1/#listbox_roles_states_props)

| Role            | Attribute                        | Element | Usage                                                        |
| --------------- | -------------------------------- | ------- | ------------------------------------------------------------ |
| `listbox`       |                                  | `ul`    | Identifies the focusable element that has listbox behaviors and contains the listbox options. |
|                 | `aria-labelledby="ID_REF"`       | `ul`    | Refers to the element containing the listbox label.          |
|                 | `tabindex="0"`                   | `ul`    | Includes the listbox in the page tab sequence.               |
|                 | `aria-activedescendant="ID_REF"` | `ul`    | 1. Tells assistive technologies which of the options, if any, is visually indicated as having keyboard focus.<br/>2. DOM focus remains on the `ul` element and the idref specified for `aria-activedescendant` refers to the `li` element that is visually styled as focused.<br/>3. When navigation keys, such as Down Arrow, are pressed, the JavaScript changes the value. |
| `role="option"` |                                  | `li`    | Identifies each selectable element containing the name of an option. |
|                 | `aria-selected="true"`           | `li`    | 1. Indicates that the option is selected.<br/>2. Applied to the element with role option that is visually styled as selected.<br/>3. The option with this attribute is always the same as the option that is referenced by aria-activedescendant because it is a single-select listbox where selection follows focus. |
