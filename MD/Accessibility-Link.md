# Link
A [link](https://www.w3.org/TR/wai-aria-1.1/#link) widget provides an interactive reference to a resource. The target resource can be either external or local, i.e., either outside or within the current page or application.

## Attention
**Authors are strongly encouraged to use a native host language link element, such as an HTML `<A>` element with an `href` attribute.** As with other WAI-ARIA widget roles, applying the link role to an element will not cause browsers to enhance the element with standard link behaviors, such as navigation to the link target or context menu actions. When using the `link` role, providing these features of the element is the author's responsibility.

## Keyboard Support

| Key   | Function            |
| ----- | ------------------- |
| enter | Activates the link. |

## Role, Property, State, and Tabindex Attributes

| Role   | Attribute      | Element       | Usage                                                        |
| ------ | -------------- | ------------- | ------------------------------------------------------------ |
| `link` |                | `span` `img`  | Examples 1 and 3: Identifies the `span` element as a `link`.<br/>Example 2: Identifies the `img` element as a `link`. |
|        | `tabindex="0"` | `span`, `img` | Includes the link element in the page tab sequence.          |
|        | `alt`          | `img`         | Example 2: Defines the accessible name of the link.          |
|        | `aria-label`   | `span`        | Example 3: Defines the accessible name of the link.          |

## Basic Example - HTML
```
<span
  tabindex="0"
  role="link"
  onclick="goToLink(event, 'http://www.w3.org/')"
  onkeydown="goToLink(event, 'http://www.w3.org/')"
>
  W3C website
</span>
<img
  tabindex="0"
  role="link"
  onclick="goToLink(event, 'http://www.w3.org/')"
  onkeydown="goToLink(event, 'http://www.w3.org/')"
  src="./w3c-logo.png"
  alt="W3C Website"
/>
<span
  tabindex="0"
  role="link"
  class="link3"
  onclick="goToLink(event, 'http://www.w3.org/TR/wai-aria-practices/')"
  onkeydown="goToLink(event, 'http://www.w3.org/TR/wai-aria-practices/')"
  aria-label="W3C website"
></span>
```