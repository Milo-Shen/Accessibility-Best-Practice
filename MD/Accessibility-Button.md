# Button
A `button ` is a widget that enables users to trigger an action or event, such as submitting a form, opening a dialog, canceling an action, or performing a delete operation. A common convention for informing users that a button launches a dialog is to append "…" (ellipsis) to the button label, e.g., "Save as…".

## Two other types of buttons
1. Toggle button: A two-state button that can be either off (not pressed) or on (pressed). To tell assistive technologies that a button is a toggle button, specify a value for the attribute [aria-pressed](https://www.w3.org/TR/wai-aria-1.1/#aria-pressed). For example, a button labelled mute in an audio player could indicate that sound is muted by setting the pressed state true. **Important:** it is critical the label on a toggle does not change when its state changes. In this example, when the pressed state is true, the label remains "Mute" so a screen reader would say something like "Mute toggle button pressed". Alternatively, if the design were to call for the button label to change from "Mute" to "Unmute," the aria-pressed attribute would not be needed.
2. Menu button: as described in the [menu button pattern](https://www.w3.org/TR/wai-aria-practices-1.1/#menubutton), a button is revealed to assistive technologies as a menu button if it has the property [aria-haspopup](https://www.w3.org/TR/wai-aria-1.1/#aria-haspopup) set to either `menu` or `true`.

## Behavior
1. An input that allows for user-triggered actions when clicked or pressed. See related [`link`](https://www.w3.org/TR/wai-aria-1.1/#link).
2. Buttons are mostly used for discrete actions. Standardizing the appearance of buttons enhances the user's recognition of the [widgets](https://www.w3.org/TR/wai-aria-1.1/#dfn-widget) as buttons and allows for a more compact display in toolbars.
3. Buttons support the optional [attribute](https://www.w3.org/TR/wai-aria-1.1/#dfn-attribute) [`aria-pressed`](https://www.w3.org/TR/wai-aria-1.1/#aria-pressed). Buttons with a non-empty `aria-pressed` attribute are toggle buttons. When `aria-pressed` is `true` the button is in a "pressed" [state](https://www.w3.org/TR/wai-aria-1.1/#dfn-state), when `aria-pressed` is `false` it is not pressed. If the attribute is not present, the button is a simple command button.

## Note 
The types of actions performed by buttons are distinctly different from the function of a link (see [link pattern](https://www.w3.org/TR/wai-aria-practices-1.1/#link)). It is important that both the appearance and role of a widget match the function it provides. Nevertheless, elements occasionally have the visual style of a link but perform the action of a button. In such cases, giving the element role `button` helps assistive technology users understand the function of the element. However, a better solution is to adjust the visual design so it matches the function and ARIA role.

## Keyboard Support
| Key   | Function              |
| ----- | --------------------- |
| Enter | Activates the button. |
| Space | Activates the button. |

### When the button has focus:

- Space: Activates the button.
- Enter: Activates the button.
- Following button activation, focus is set depending on the type of action the button performs. For example:
  - If activating the button opens a dialog, the focus moves inside the dialog. (see [dialog pattern](https://www.w3.org/TR/wai-aria-practices-1.1/#dialog_modal))
  - If activating the button closes a dialog, focus typically returns to the button that opened the dialog unless the function performed in the dialog context logically leads to a different element. For example, activating a cancel button in a dialog returns focus to the button that opened the dialog. However, if the dialog were confirming the action of deleting the page from which it was opened, the focus would logically move to a new context.
  - If activating the button does not dismiss the current context, then focus typically remains on the button after activation, e.g., an Apply or Recalculate button.
  - If the button action indicates a context change, such as move to next step in a wizard or add another search criteria, then it is often appropriate to move focus to the starting point for that action.
  - If the button is activated with a shortcut key, the focus usually remains in the context from which the shortcut key was activated. For example, if Alt + U were assigned to an "Up" button that moves the currently focused item in a list one position higher in the list, pressing Alt + U when the focus is in the list would not move the focus from the list.

## Role, Property, State, and Tabindex Attributes

| Role     | Attribute              | Element    | Usage                                                        |
| -------- | ---------------------- | ---------- | ------------------------------------------------------------ |
| `button` |                        | `div`, `a` | Identifies the element as a `button` widget.Accessible name for the button is defined by the text content of the element. |
|          | `tabindex="0"`         | `div`, `a` | Includes the element in the tab sequence.Needed on the `a` element because it does not have a `href` attribute. |
|          | `aria-pressed="false"` | `a`        | Identifies the button as a toggle button.Indicates the toggle button is not pressed. |
|          | `aria-pressed="true"`  | `a`        | Identifies the button as a toggle button.Indicates the toggle button is pressed. |

## Questions
1. `aria-pressed` is also take effect on `div` element. Can we use it ?

## Attention 
1. require accessible name
2. `tabindex="0"` is needed on the `a` element because it does not have a href attribute.
3. <font color='red'>`preventDefault()` muse be called the `keydown` and `keyup` event are triggered by space. The action button is activated by space on the `keyup or keydown` event, but the default action for space is already triggered on keydown. It needs to be prevented to stop scrolling the page before activating the button.</font>

## Example
[Button Accessibility Example Website](https://www.w3.org/TR/wai-aria-practices-1.1/examples/button/button.html)

### html

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Title</title>
    <link rel="stylesheet" href="index.css" />
  </head>
  <body>
    <p>
      This
      <q>
        Print
      </q>
      action button uses a
      <code>
        div
      </code>
      element.
    </p>
    <div tabindex="0" role="button" id="action">
      Print Page
    </div>
    <p>
      This
      <q>
        Mute
      </q>
      toggle button uses an
      <code>
        a
      </code>
      element.
    </p>
    <a tabindex="0" role="button" id="toggle" aria-pressed="false">
      Mute
      <svg>
        <use xlink:href="images/mute.svg#icon-sound"></use>
      </svg>
    </a>
    <p>
      This
      <q>
        Mute
      </q>
      toggle button uses an
      <code>
        button
      </code>
      element.
    </p>
    <div tabindex="0" role="button" id="toggleBtn" aria-pressed="false">
      My Div Mute
      <svg>
        <use xlink:href="images/mute.svg#icon-sound"></use>
      </svg>
    </div>
    <script type="text/javascript" src="checkboxMixed.js"></script>
  </body>
</html>
```

### javascript

```
/*
 *   This content is licensed according to the W3C Software License at
 *   https://www.w3.org/Consortium/Legal/2015/copyright-software-and-document
 *
 *   JS code for the button design pattern
 */

var ICON_MUTE_URL = "images/mute.svg#icon-mute";
var ICON_SOUND_URL = "images/mute.svg#icon-sound";

function init() {
  var actionButton = document.getElementById("action");
  actionButton.addEventListener("click", activateActionButton);
  actionButton.addEventListener("keydown", actionButtonKeydownHandler);
  actionButton.addEventListener("keyup", actionButtonKeyupHandler);

  var toggleButton = document.getElementById("toggle");
  toggleButton.addEventListener("click", toggleButtonClickHandler);
  toggleButton.addEventListener("keydown", toggleButtonKeydownHandler);
  toggleButton.addEventListener("keyup", toggleButtonKeyupHandler);

  var toggleBtn = document.getElementById("toggleBtn");
  toggleBtn.addEventListener("click", toggleButtonClickHandler);
  toggleBtn.addEventListener("keydown", toggleButtonKeydownHandler);
  toggleBtn.addEventListener("keyup", toggleButtonKeyupHandler);
}

/**
 * Activates the action button with the enter key.
 *
 * @param {KeyboardEvent} event
 */
function actionButtonKeydownHandler(event) {
  // The action button is activated by space on the keyup event, but the
  // default action for space is already triggered on keydown. It needs to be
  // prevented to stop scrolling the page before activating the button.
  if (event.keyCode === 32) {
    event.preventDefault();
  }
  // If enter is pressed, activate the button
  else if (event.keyCode === 13) {
    event.preventDefault();
    activateActionButton();
  }
}

/**
 * Activates the action button with the space key.
 *
 * @param {KeyboardEvent} event
 */
function actionButtonKeyupHandler(event) {
  if (event.keyCode === 32) {
    event.preventDefault();
    activateActionButton();
  }
}

function activateActionButton() {
  window.print();
}

/**
 * Toggles the toggle button’s state if it’s actually a button element or has
 * the `role` attribute set to `button`.
 *
 * @param {MouseEvent} event
 */
function toggleButtonClickHandler(event) {
  if (
    event.currentTarget.tagName === "button" ||
    event.currentTarget.getAttribute("role") === "button"
  ) {
    toggleButtonState(event.currentTarget);
  }
}

/**
 * Toggles the toggle button’s state with the enter key.
 *
 * @param {KeyboardEvent} event
 */
function toggleButtonKeydownHandler(event) {
  if (event.keyCode === 32) {
    event.preventDefault();
  } else if (event.keyCode === 13) {
    event.preventDefault();
    toggleButtonState(event.currentTarget);
  }
}

/**
 * Toggles the toggle button’s state with space key.
 *
 * @param {KeyboardEvent} event
 */
function toggleButtonKeyupHandler(event) {
  if (event.keyCode === 32) {
    event.preventDefault();
    toggleButtonState(event.currentTarget);
  }
}

/**
 * Toggles the toggle button’s state between *pressed* and *not pressed*.
 *
 * @param {HTMLElement} button
 */
function toggleButtonState(button) {
  var isAriaPressed = button.getAttribute("aria-pressed") === "true";

  button.setAttribute("aria-pressed", isAriaPressed ? "false" : "true");

  var icon = button.querySelector("use");
  icon.setAttribute(
    "xlink:href",
    isAriaPressed ? ICON_SOUND_URL : ICON_MUTE_URL
  );
}

window.onload = init;
```

### css

```
[role="button"] {
  display: inline-block;
  position: relative;
  padding: 0.4em 0.7em;
  border: 1px solid hsl(213, 71%, 49%);
  border-radius: 5px;
  box-shadow: 0 1px 2px hsl(216, 27%, 55%);
  color: #fff;
  text-shadow: 0 -1px 1px hsl(216, 27%, 25%);
  background-color: hsl(216, 82%, 51%);
  background-image: linear-gradient(
    to bottom,
    hsl(216, 82%, 53%),
    hsl(216, 82%, 47%)
  );
}

[role="button"]:hover {
  border-color: hsl(213, 71%, 29%);
  background-color: hsl(216, 82%, 31%);
  background-image: linear-gradient(
    to bottom,
    hsl(216, 82%, 33%),
    hsl(216, 82%, 27%)
  );
  cursor: default;
}

[role="button"]:focus {
  outline: none;
}

[role="button"]:focus::before {
  position: absolute;
  z-index: -1;

  /* button border width - outline width - offset */
  top: calc(-1px - 3px - 3px);
  right: calc(-1px - 3px - 3px);
  bottom: calc(-1px - 3px - 3px);
  left: calc(-1px - 3px - 3px);
  border: 3px solid hsl(213, 71%, 49%);

  /* button border radius + outline width + offset */
  border-radius: calc(5px + 3px + 3px);
  content: "";
}

[role="button"]:active {
  border-color: hsl(213, 71%, 49%);
  background-color: hsl(216, 82%, 31%);
  background-image: linear-gradient(
    to bottom,
    hsl(216, 82%, 53%),
    hsl(216, 82%, 47%)
  );
  box-shadow: inset 0 3px 5px 1px hsl(216, 82%, 30%);
}

[role="button"][aria-pressed] {
  border-color: hsl(261, 71%, 49%);
  box-shadow: 0 1px 2px hsl(261, 27%, 55%);
  text-shadow: 0 -1px 1px hsl(261, 27%, 25%);
  background-color: hsl(261, 82%, 51%);
  background-image: linear-gradient(
    to bottom,
    hsl(261, 82%, 53%),
    hsl(261, 82%, 47%)
  );
}

[role="button"][aria-pressed]:hover {
  border-color: hsl(261, 71%, 29%);
  background-color: hsl(261, 82%, 31%);
  background-image: linear-gradient(
    to bottom,
    hsl(261, 82%, 33%),
    hsl(261, 82%, 27%)
  );
}

[role="button"][aria-pressed="true"] {
  padding-top: 0.5em;
  padding-bottom: 0.3em;
  border-color: hsl(261, 71%, 49%);
  background-color: hsl(261, 82%, 31%);
  background-image: linear-gradient(
    to bottom,
    hsl(261, 82%, 63%),
    hsl(261, 82%, 57%)
  );
  box-shadow: inset 0 3px 5px 1px hsl(261, 82%, 30%);
}

[role="button"][aria-pressed="true"]:hover {
  border-color: hsl(261, 71%, 49%);
  background-color: hsl(261, 82%, 31%);
  background-image: linear-gradient(
    to bottom,
    hsl(261, 82%, 43%),
    hsl(261, 82%, 37%)
  );
  box-shadow: inset 0 3px 5px 1px hsl(261, 82%, 20%);
}

[role="button"][aria-pressed]:focus::before {
  border-color: hsl(261, 71%, 49%);
}

[role="button"] svg {
  margin: 0.15em auto -0.15em;
  height: 1em;
  width: 1em;
  pointer-events: none;
}
```