# Checkbox
WAI-ARIA supports two types of [checkbox](https://www.w3.org/TR/wai-aria-1.1/#checkbox) widgets:

1. Dual-state: The most common type of checkbox, it allows the user to toggle between two choices -- checked and not checked.
2. Tri-state: This type of checkbox supports an additional third state known as partially checked.

One common use of a tri-state checkbox can be found in software installers where a single tri-state checkbox is used to represent and control the state of an entire group of install options. And, each option in the group can be individually turned on or off with a dual state checkbox.

1. If all options in the group are checked, the overall state is represented by the tri-state checkbox displaying as checked.
2. If some of the options in the group are checked, the overall state is represented with the tri-state checkbox displaying as partially checked.
3. If none of the options in the group are checked, the overall state of the group is represented with the tri-state checkbox displaying as not checked.

The user can use the tri-state checkbox to change all options in the group with a single action:

1. Checking the overall checkbox checks all options in the group.
2. Unchecking the overall checkbox will uncheck all options in the group.
3. And, In some implementations, the system may remember which options were checked the last time the overall status was partially checked. If this feature is provided, activating the overall checkbox a third time recreates that partially checked state where only some options in the group are checked.

## Attention
1. Accessible Name Required
2. Children Presentational
3. default value of `aria-checked` is `false`
 
## Characteristics

| Characteristic                   | Value                                                        |
| -------------------------------- | ------------------------------------------------------------ |
| Superclass Role:                 | [`input`](https://www.w3.org/TR/wai-aria-1.1/#input)         |
| Subclass Roles:                  | [`menuitemcheckbox`](https://www.w3.org/TR/wai-aria-1.1/#menuitemcheckbox)<br/>[`switch`](https://www.w3.org/TR/wai-aria-1.1/#switch) |
| Related Concepts:                | [HTML `input[type="checkbox"\]`](https://www.w3.org/TR/html5/sec-forms.html#checkbox-state-typecheckbox)<br/>[`option`](https://www.w3.org/TR/wai-aria-1.1/#option) |
| Required States and Properties:  | [`aria-checked`](https://www.w3.org/TR/wai-aria-1.1/#aria-checked) |
| Supported States and Properties: | [`aria-readonly`](https://www.w3.org/TR/wai-aria-1.1/#aria-readonly) |
| Name From:                       | contents<br/>author                                          |
| Accessible Name Required:        | True                                                         |
| Children Presentational:         | True                                                         |
| Implicit Value for Role:         | Default for [`aria-checked`](https://www.w3.org/TR/wai-aria-1.1/#aria-checked) is `false`. |


  
## WAI-ARIA Roles, States, and Properties

- The checkbox has role [checkbox](https://www.w3.org/TR/wai-aria-1.1/#checkbox).
- The checkbox has an accessible label provided by one of the following:
  - Visible text content contained within the element with role `checkbox`.
  - A visible label referenced by the value of [aria-labelledby](https://www.w3.org/TR/wai-aria-1.1/#aria-labelledby) set on the element with role `checkbox`.
  - [aria-label](https://www.w3.org/TR/wai-aria-1.1/#aria-label) set on the element with role `checkbox`.
- When checked, the checkbox element has state [aria-checked](https://www.w3.org/TR/wai-aria-1.1/#aria-checked) set to `true`.
- When not checked, it has state [aria-checked](https://www.w3.org/TR/wai-aria-1.1/#aria-checked) set to `false`.
- When partially checked, it has state [aria-checked](https://www.w3.org/TR/wai-aria-1.1/#aria-checked) set to `mixed`.
- If a set of checkboxes is presented as a logical group with a visible label, the checkboxes are included in an element with role [group](https://www.w3.org/TR/wai-aria-1.1/#group) that has the property [aria-labelledby](https://www.w3.org/TR/wai-aria-1.1/#aria-labelledby) set to the ID of the element containing the label.
- If the presentation includes additional descriptive static text relevant to a checkbox or checkbox group, the checkbox or checkbox group has the property [aria-describedby](https://www.w3.org/TR/wai-aria-1.1/#aria-describedby) set to the ID of the element containing the description.   
   
## Two-State Checkbox

### Keyboard Support

| Key   | Function                                               |
| ----- | ------------------------------------------------------ |
| Tab   | Moves keyboard focus to the `checkbox`.                |
| Space | Toggles checkbox between checked and unchecked states. |

### Role, Property, State, and Tabindex Attributes

| Role       | Attribute              | Element | Usage                                                        |
| ---------- | ---------------------- | ------- | ------------------------------------------------------------ |
|            |                        | `h3`    | Provides a grouping label for the group of checkboxes.       |
| `group`    |                        | `div`   | Identifies the `div` element as a `group` container for the checkboxes. |
|            | `aria-labelledby`      | `div`   | The `aria-labelledby` attribute references the `id` attribute of the `h3` element to define the accessible name for the group of checkboxes. |
| `checkbox` |                        | `div`   | Identifies the `div` element as a `checkbox`.The child text content of this `div` provides the accessible name of the checkbox. |
|            | `tabindex="0"`         | `div`   | Includes the checkbox in the page tab sequence.              |
|            | `aria-checked="false"` | `div`   | Indicates the `checkbox` is **not** checked.CSS attribute selectors (e.g. `[aria-checked="false"]`) are used to synchronize the visual states with the value of the `aria-checked` attribute.To support operating system and browser high contrast settings, the CSS `::before` pseudo element and `content` property are used to generate the visual indicators of the checkbox state. |
|            | `aria-checked="true"`  | `div`   | Indicates the `checkbox` is checked.CSS attribute selectors (e.g. `[aria-checked="true"]`) are used to synchronize the visual states with the value of the `aria-checked` attribute.To support operating system and browser high contrast settings, the CSS `::before` pseudo element and `content` property are used to generate the visual indicators of the checkbox state. |

### Two-State Checkbox Example
[Two-State Checkbox Example Website](https://www.w3.org/TR/wai-aria-practices-1.1/examples/checkbox/checkbox-1/checkbox-1.html)

## Tri-State Checkbox

### Keyboard Support
## Keyboard Support

| Key   | Function                                                     |
| ----- | ------------------------------------------------------------ |
| Tab   | Moves keyboard focus among the checkboxes.                   |
| Space | Cycles the tri-state checkbox among unchecked, mixed, and checked states.When the tri-state checkbox is unchecked, all the controlled checkboxes are unchecked.When the tri-state checkbox is mixed, the controlled checkboxes return to the last combination of states they had when the tri-state checkbox was last mixed or to the default combination of states they had when the page loaded.When the tri-state checkbox is checked, all the controlled checkboxes are checked. |

## Role, Property, State, and Tabindex Attributes

| Role       | Attribute                  | Element | Usage                                                        |
| ---------- | -------------------------- | ------- | ------------------------------------------------------------ |
| `checkbox` |                            | `div`   | 1. Identifies the `div` element as a `checkbox`.<br/>2. The child text content of this `div` provides the accessible name of the checkbox. |
|            | `tabindex="0"`             | `div`   | Includes the checkbox in the page tab sequence.              |
|            | `aria-controls="[IDREFS]"` | `div`   | identifies the set of checkboxes controlled by the mixed checkbox. |
|            | `aria-checked="false"`     | `div`   | 1. Indicates the tri-state `checkbox` is **not** checked.<br/>2. In this state, all controlled checkboxes are unchecked.<br/>3. CSS attribute selectors (e.g. `[aria-checked="false"]`) are used to synchronize the visual states with the value of the `aria-checked` attribute.<br/>4. To support operating system and browser high contrast settings, the CSS `::before` pseudo element and `content` property are used to generate the visual indicators of the checkbox state. |
|            | `aria-checked="true"`      | `div`   | 1. Indicates the tri-state `checkbox` is checked.<br/>2. In this state, all controlled checkboxes are checked.<br/>3. CSS attribute selectors (e.g. `[aria-checked="true"]`) are used to synchronize the visual states with the value of the `aria-checked` attribute.<br/>4. To support operating system and browser high contrast settings, the CSS `::before` pseudo element and `content` property are used to generate the visual indicators of the checkbox state. |
|            | `aria-checked="mixed"`     | `div`   | 1. Indicates the tri-state `checkbox` is mixed.<br/>2. In this state, some controlled checkboxes are unchecked and some are checked.<br/>3. CSS attribute selectors (e.g. `[aria-checked="mixed"]`) are used to synchronize the visual states with the value of the `aria-checked` attribute.<br/>4. To support operating system and browser high contrast settings, the CSS `::before` pseudo element and `content` property are used to generate the visual indicators of the checkbox state. |