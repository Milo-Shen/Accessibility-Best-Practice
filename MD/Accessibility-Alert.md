# Alert
An alert is an element that displays a brief, important, and potentially time-sensitive message in a way that attracts the user's attention without interrupting the user's task. 

## Accessibility Features
Because an alert is for critical information, assistive technologies may provide special behaviors designed to help call attention to changes in the text of an alert. For example, screen readers may interrupt all other speech and preface announcement of the new alert text with a special sound or phrase.

## Behavior
1. Dynamically rendered alerts are automatically announced by most screen readers
2. In some operating systems, they may trigger an alert sound ( Optional )
3. screen readers do not inform users of alerts that are present on the page before page load completes
4. Alert do not affect keyboard focus ( The alert dialog is designed for situations where interrupting work flow is necessary )
5. Avoid designing alerts that disappear automatically
6. Consideration the frequency of interruption caused by alerts

## Keyboard Support
No keyboard interaction needed.

## Attention
It is also important to avoid designing alerts that disappear automatically. An alert that disappears too quickly can lead to failure to meet WCAG 2.0 success criterion 2.2.3. Another critical design consideration is the frequency of interruption caused by alerts. Frequent interruptions inhibit usability for people with visual and cognitive disabilities, which makes meeting the requirements of WCAG 2.0 success criterion 2.2.4 more difficult.

## Role, Property, State, and Tabindex Attributes
| Role    | Attribute             | Element           | Usage                                                        |
| ------- | --------------------- | ----------------- | ------------------------------------------------------------ |
| `alert` |                       | `div`             | Identifies the element as the container where alert content will be added or updated. |
|         | `aria-live=assertive` | Implicit on `div` | 1. This does not have to be declared in the code because it is implicit in the alert role.<br/> 2. Tells assistive technologies to interrupt other processes to provide users with immediate notification of relevant alert container changes. |
|         | `aria-atomic=true`    | Implicit on `div` | 1. This does not have to be declared in the code because it is implicit in the alert role. <br/> 2. Tells assistive technologies to use the entire content of the alert element as the alert message even if only a portion of it has changed. |

## Implicit Value for Role
1. Default for aria-live is assertive
2. Default for aria-atomic is true

## Example

[Alert Accessibility Example Website](https://www.w3.org/TR/wai-aria-practices-1.1/examples/alert/alert.html)

```html
<div role="alert" aria-live="assertive">
    <p>
        <span lang="da">Hej</span>, hello,
        <span lang="it">ciao</span>,
        <span lang="ja">こんにちは</span>,
        <span lang="ko">안녕</span>
    </p>
</div>
```