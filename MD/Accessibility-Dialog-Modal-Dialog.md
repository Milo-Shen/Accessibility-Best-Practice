# Dialog ( Modal ) Example
The below Add Delivery Address button opens a modal dialog that contains two buttons that open other dialogs. The accessibility features section explains the rationale for initial focus placement and use of `aria-describedby` in each dialog.

## Accessibility Features

1. To make the content easier to read when displayed on small screens, the dialog fills 100% of the screen. Completely covering the background window also hides background movement that occurs on some mobile devices when scrolling content inside the dialog.
2. Focus and accessible descriptions are set based on the content of each dialog.
   1. Add Delivery Address dialog (id=dialog1):
      - Initial focus is set on the first input, which is the first focusable element.
      - The dialog does not need `aria-describedby` since there is no static text that describes it.
      - When the dialog closes as a result of the Cancel action, the user's point of regard is maintained by returning focus to the Add Delivery Address button.
      - When the dialog closes as a result of the Add action and the Address Added dialog replaces the Add Delivery Address dialog, the Add Delivery Address dialog passes a reference to the Add Delivery Address button to the Address Added dialog so that it can maintain the user's point of regard when it closes.
   2. Verification Result dialog (id=dialog2):
      - Initial focus is set on the first paragraph because the first interactive element is at the bottom, which is out of view due to the length of the text.
      - To support screen reader user awareness of the dialog text, the dialog text is wrapped in a `div` that is referenced by `aria-describedby`.
      - When the dialog closes, to maintain the user's point of regard, focus returns to the Verify Address button.
      - The text of this dialog describes design considerations for initial focus and accessible descriptions in dialogs with large amounts of text.
   3. Address Added dialog (id=dialog3):
      - Initial focus is set on the OK button, which is the last focusable element. This is for efficiency since most users will simply dismiss the dialog as soon as they have read the message. Users can press Tab to focus on the My Profile link.
      - The element containing the dialog message is referenced by `aria-describedby` to hint to screen readers that it should be announced when the dialog opens.
      - When the dialog closes, the user's point of regard is maintained by setting focus on the Add Delivery Address button.
   4. End of the Road!  dialog (id=dialog4):
      - This dialog has only one focusable element, which receives focus when the dialog opens.
      - Like dialog3, `aria-describedby` is used to facilitate message announcement for screen reader users.
      - Like all other dialogs in this example except for the Address Added confirmation dialog, when it closes, the user's point of regard is maintained by returning focus to the element that triggered display of the dialog.

## Keyboard Support

| Key         | Function                                                     |
| ----------- | ------------------------------------------------------------ |
| Tab         | 1. Moves focus to next focusable element inside the dialog.<br/>2. When focus is on the last focusable element in the dialog, moves focus to the first focusable element in the dialog. |
| Shift + Tab | 1. Moves focus to previous focusable element inside the dialog.<br/>2. When focus is on the first focusable element in the dialog, moves focus to the last focusable element in the dialog. |
| Escape      | Closes the dialog.                                           |

## Role, Property, State, and Tabindex Attributes

| Role     | Attribute                | Element | Usage                                                        |
| -------- | ------------------------ | ------- | ------------------------------------------------------------ |
| `dialog` |                          | `div`   | Identifies the element that serves as the dialog container.  |
|          | `aria-labelledby=IDREF`  | `div`   | Gives the dialog an accessible name by referring to the element that provides the dialog title. |
|          | `aria-describedby=IDREF` | `div`   | 1. Gives the dialog an accessible description by referring to the dialog content that describes the primary message or purpose of the dialog.<br/>2. Used in three of the four dialogs included in the example. See the above accessibility features section for an explanation. |
|          | `aria-modal=true`        | `div`   | Tells assistive technologies that the windows underneath the current dialog are not available for interaction (inert). |

### Notes on `aria-modal` and `aria-hidden`

1. The `aria-modal` property was introduced in ARIA 1.1. As a new property, screen reader users may experience varying degrees of support for it.
2. Applying the `aria-modal` property to the `dialog` element replaces the technique of using `aria-hidden` on the background for informing assistive technologies that content outside a dialog is inert.
3. In legacy dialog implementations where `aria-hidden` is used to make content outside a dialog inert for assistive technology users, it is important that:
   1. `aria-hidden` is set to `true` on each element containing a portion of the inert layer.
   2. The dialog element is not a descendant of any element that has `aria-hidden` set to `true`.

## Basic Example - HTML
```
<button onclick="openDialog('dialog1', this)">
  Add Delivery Address
</button>
<div
  role="dialog"
  id="dialog1"
  aria-labelledby="dialog1_label"
  aria-modal="true"
  class="hidden"
>
  <h2 id="dialog1_label" class="dialog_label">
    Add Delivery Address
  </h2>
  <div class="dialog_form">
    <div class="dialog_form_item">
      <label>
        <span class="label_text">
          Street:
        </span>
        <input type="text" class="wide_input" />
      </label>
    </div>
    <div class="dialog_form_item">
      <label>
        <span class="label_text">
          City:
        </span>
        <input type="text" class="city_input" />
      </label>
    </div>
    <div class="dialog_form_item">
      <label>
        <span class="label_text">
          State:
        </span>
        <input type="text" class="state_input" />
      </label>
    </div>
    <div class="dialog_form_item">
      <label>
        <span class="label_text">
          Zip:
        </span>
        <input type="text" class="zip_input" />
      </label>
    </div>
    <div class="dialog_form_item">
      <label for="special_instructions">
        <span class="label_text">
          Special instructions:
        </span>
      </label>
      <input
        id="special_instructions"
        type="text"
        aria-describedby="special_instructions_desc"
        class="wide_input"
      />
      <div class="label_info" id="special_instructions_desc">
        For example, gate code or other information to help the driver find
        you
      </div>
    </div>
  </div>
  <div class="dialog_form_actions">
    <button onclick="openDialog('dialog2', this, 'dialog2_para1')">
      Verify Address
    </button>
    <button
      onclick="replaceDialog('dialog3', undefined, 'dialog3_close_btn')"
    >
      Add
    </button>
    <button onclick="closeDialog(this)">
      Cancel
    </button>
  </div>
</div>
<!--  Second modal to open on top of the first modal  -->
<div
  id="dialog2"
  role="dialog"
  aria-labelledby="dialog2_label"
  aria-describedby="dialog2_desc"
  aria-modal="true"
  class="hidden"
>
  <h2 id="dialog2_label" class="dialog_label">
    Verification Result
  </h2>
  <div id="dialog2_desc" class="dialog_desc">
    <p tabindex="-1" id="dialog2_para1">
      This is just a demonstration. If it were a real application, it would
      provide a message telling whether the entered address is valid.
    </p>
    <p>
      For demonstration purposes, this dialog has a lot of text. It
      demonstrates a scenario where:
    </p>
    <ul>
      <li>
        The first interactive element, the help link, is at the bottom of
        the dialog.
      </li>
      <li>
        If focus is placed on the first interactive element when the dialog
        opens, the validation message may not be visible.
      </li>
      <li>
        If the validation message is visible and the focus is on the help
        link, then the focus may not be visible.
      </li>
      <li>
        When the dialog opens, it is important that both:
        <ul>
          <li>
            The beginning of the text is visible so users do not have to
            scroll back to start reading.
          </li>
          <li>
            The keyboard focus always remains visible.
          </li>
        </ul>
      </li>
    </ul>
    <p>
      There are several ways to resolve this issue:
    </p>
    <ul>
      <li>
        Place an interactive element at the top of the dialog, e.g., a
        button or link.
      </li>
      <li>
        Make a static element focusable, e.g., the dialog title or the first
        block of text.
      </li>
    </ul>
    <p>
      Please
      <em>
        DO NOT
      </em>
      make the element with role dialog focusable!
    </p>
    <ul>
      <li>
        The larger a focusable element is, the more difficult it is to
        visually identify the location of focus, especially for users with a
        narrow field of view.
      </li>
      <li>
        The dialog has a visual border, so creating a clear visual indicator
        of focus when the entire dialog has focus is not very feasible.
      </li>
      <li>
        Screen readers read the label and content of focusable elements. The
        dialog contains its label and a lot of content! If a dialog like
        this one has focus, the actual focus is difficult to comprehend.
      </li>
    </ul>
    <p>
      In this dialog, the first paragraph has
      <code>
        tabindex=
        <q>
          -1
        </q>
      </code>
      . The first paragraph is also contained inside the element that
      provides the dialog description, i.e., the element that is referenced
      by
      <code>
        aria-describedby
      </code>
      . With some screen readers, this may have one negative but relatively
      insignificant side effect when the dialog opens -- the first paragraph
      may be announced twice. Nonetheless, making the first paragraph
      focusable and setting the initial focus on it is the most broadly
      accessible option.
    </p>
  </div>
  <div class="dialog_form_actions">
    <a href="#" onclick="openDialog('dialog4', this)">
      link to help
    </a>
    <button onclick="openDialog('dialog4', this)">
      accepting an alternative form
    </button>
    <button onclick="closeDialog(this)">
      Close
    </button>
  </div>
</div>
<!--  Dialog that replaces dialog 1.  -->
<div
  id="dialog3"
  role="dialog"
  aria-labelledby="dialog3_label"
  aria-describedby="dialog3_desc"
  aria-modal="true"
  class="hidden"
>
  <h2 id="dialog3_label" class="dialog_label">
    Address Added
  </h2>
  <p id="dialog3_desc" class="dialog_desc">
    The address you provided has been added to your list of delivery
    addresses. It is ready for immediate use. If you wish to remove it, you
    can do so from
    <a href="#" onclick="openDialog('dialog4', this)">
      your profile.
    </a>
  </p>
  <div class="dialog_form_actions">
    <button id="dialog3_close_btn" onclick="closeDialog(this)">
      OK
    </button>
  </div>
</div>
<div
  id="dialog4"
  role="dialog"
  aria-labelledby="dialog4_label"
  aria-describedby="dialog4_desc"
  class="hidden"
  aria-modal="true"
>
  <h2 id="dialog4_label" class="dialog_label">
    End of the Road!
  </h2>
  <p id="dialog4_desc" class="dialog_desc">
    You activated a fake link or button that goes nowhere! The link or
    button is present for demonstration purposes only.
  </p>
  <div class="dialog_form_actions">
    <button id="dialog4_close_btn" onclick="closeDialog(this)">
      Close
    </button>
  </div>
</div>
```