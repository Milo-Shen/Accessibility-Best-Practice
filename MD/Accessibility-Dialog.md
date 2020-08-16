# Dialog ( Modal )
A dialog is a window overlaid on either the primary window or another dialog window. Windows under a modal dialog are inert. That is, users cannot interact with content outside an active dialog window. Inert content outside an active dialog is typically visually obscured or dimmed so it is difficult to discern, and in some implementations, attempts to interact with the inert content cause the dialog to close.  

Like non-modal dialogs, modal dialogs contain their tab sequence. That is, Tab and Shift + Tab do not move focus outside the dialog. However, unlike most non-modal dialogs, modal dialogs do not provide means for moving keyboard focus outside the dialog window without closing the dialog.  

The [alertdialog](https://www.w3.org/TR/wai-aria-1.1/#alertdialog) role is a special-case dialog role designed specifically for dialogs that divert users' attention to a brief, important message. Its usage is described in the [alert dialog design pattern.](https://www.w3.org/TR/wai-aria-practices-1.1/#alertdialog)

## Usage
Dialogs are most often used to prompt the user to enter or respond to information. A dialog that is designed to interrupt workflow is usually modal. See related [`alertdialog`](https://www.w3.org/TR/wai-aria-1.1/#alertdialog).

## Attention
1. Authors *SHOULD* provide a dialog label, which can be done with the [`aria-label`](https://www.w3.org/TR/wai-aria-1.1/#aria-label) or [`aria-labelledby`](https://www.w3.org/TR/wai-aria-1.1/#aria-labelledby) attribute.

2. Authors *SHOULD* ensure that all dialogs (both modal and non-modal) have at least one focusable descendant element.
3. Authors *SHOULD* focus an element in the modal dialog when it is displayed, and authors *SHOULD* manage focus of modal dialogs.

## Characteristic
| Characteristic            | Value                                                        |
| ------------------------- | ------------------------------------------------------------ |
| Superclass Role:          | [`window`](https://www.w3.org/TR/wai-aria-1.1/#window)       |
| Subclass Roles:           | [`alertdialog`](https://www.w3.org/TR/wai-aria-1.1/#alertdialog) |
| Name From:                | author                                                       |
| Accessible Name Required: | True                                                         |

## Keyboard Interaction
In the following description, the term tabbable element refers to any element with a `tabindex` value of zero or greater. Note that values greater than 0 are strongly discouraged.

- When a dialog opens, focus moves to an element inside the dialog. See notes below regarding initial focus placement.
- Tab:
  - Moves focus to the next tabbable element inside the dialog.
  - If focus is on the last tabbable element inside the dialog, moves focus to the first tabbable element inside the dialog.
- Shift + Tab:
  - Moves focus to the previous tabbable element inside the dialog.
  - If focus is on the first tabbable element inside the dialog, moves focus to the last tabbable element inside the dialog.
- Escape: Closes the dialog.

### NOTE - Keyboard Interaction

1. When a dialog opens, focus placement depends on the nature and size of the content.

   - In all circumstances, focus moves to an element contained in the dialog.
   - Unless a condition where doing otherwise is advisable, focus is initially set on the first focusable element.
   - <b>If content is large enough that focusing the first interactive element could cause the beginning of content to scroll out of view, it is advisable to add `tabindex=-1` to a static element at the top of the dialog, such as the dialog title or first paragraph, and initially focus that element.</b>
   - <b>If a dialog contains the final step in a process that is not easily reversible, such as deleting data or completing a financial transaction, it may be advisable to set focus on the least destructive action, especially if undoing the action is difficult or impossible. The [Alert Dialog Pattern](https://www.w3.org/TR/wai-aria-practices-1.1/#alertdialog) is often employed in such circumstances.</b>
   - <b>If a dialog is limited to interactions that either provide additional information or continue processing, it may be advisable to set focus to the element that is likely to be most frequently used, such as an OK or Continue button.</b>b>

2. When a dialog closes, focus returns to the element that invoked the dialog unless either:

   - The invoking element no longer exists. Then, focus is set on another element that provides logical work flow.

   - The work flow design includes the following conditions that can occasionally make focusing a different element a more logical choice:

     1. It is very unlikely users need to immediately re-invoke the dialog.
     2. The task completed in the dialog is directly related to a subsequent step in the work flow.

     For example, a grid has an associated toolbar with a button for adding rows. the Add Rows button opens a dialog that prompts for the number of rows. After the dialog closes, focus is placed in the first cell of the first new row.

3. It is strongly recommended that the tab sequence of all dialogs include a visible element with role `button` that closes the dialog, such as a close icon or cancel button.

## WAI-ARIA Roles, States, and Properties
- The element that serves as the dialog container has a role of [dialog](https://www.w3.org/TR/wai-aria-1.1/#dialog).
- All elements required to operate the dialog are descendants of the element that has role `dialog`.
- The dialog container element has [aria-modal](https://www.w3.org/TR/wai-aria-1.1/#aria-modal) set to `true`.
- The dialog has either:
  - A value set for the [aria-labelledby](https://www.w3.org/TR/wai-aria-1.1/#aria-labelledby) property that refers to a visible dialog title.
  - A label specified by [aria-label](https://www.w3.org/TR/wai-aria-1.1/#aria-label).
- Optionally, the [aria-describedby](https://www.w3.org/TR/wai-aria-1.1/#aria-describedby) property is set on the element with the `dialog` role to indicate which element or elements in the dialog contain content that describes the primary purpose or message of the dialog. <b>Specifying descriptive elements enables screen readers to announce the description along with the dialog title and initially focused element when the dialog opens.</b>

## NOTE - WAI-ARIA Roles, States, and Properties

- Because marking a dialog modal by setting [aria-modal](https://www.w3.org/TR/wai-aria-1.1/#aria-modal) to `true` can prevent users of some assistive technologies from perceiving content outside the dialog, users of those technologies will experience severe negative ramifications if a dialog is marked modal but does not behave as a modal for other users. So, mark a dialog modal **only when both:**
	1. Application code prevents all users from interacting in any way with content outside of it.
	2. Visual styling obscures the content outside of it.
- The `aria-modal` property introduced by ARIA 1.1 replaces [aria-hidden](https://www.w3.org/TR/wai-aria-1.1/#aria-hidden) for informing assistive technologies that content outside a dialog is inert. However, in legacy dialog implementations where `aria-hidden` is used to make content outside a dialog inert for assistive technology users, it is important that:
	1. `aria-hidden` is set to `true` on each element containing a portion of the inert layer.
	2. The dialog element is not a descendant of any element that has `aria-hidden` set to `true`.

