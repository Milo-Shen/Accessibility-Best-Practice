# Breadcrumb
A breadcrumb trail consists of a list of links to the parent pages of the current page in hierarchical order. It helps users find their place within a website or web application. Breadcrumbs are often placed horizontally before a page's main content.

## Accessibility Features
1. The set of links is structured using an ordered list
2. A nav element labeled Breadcrumb identifies the structure as a breadcrumb trail and makes it a navigation landmark so that it is easy to locate
3. To prevent screen reader announcement of the visual separators between links, they are added via CSS:
	1. The separators are part of the visual presentation that signifies the breadcrumb trail, which is already semantically represented by the nav element with its label of Breadcrumb. So, using a display technique that is not represented in the accessibility tree used by screen readers prevents redundant and potentially distracting verbosity
	2. Each link has a border on one side that is skewed with the CSS’ `transform ` property so it resembles a slash

## Behavior
1. A breadcrumb trail consists of a list of links to the parent pages of the current page in hierarchical order
2. Breadcrumbs are often placed horizontally before a page's main content

## Keyboard Support
No keyboard interaction needed.

## Role, Property, State, and Tabindex Attributes

| Role | Attribute               | Element | Usage                                                        |
| ---- | ----------------------- | ------- | ------------------------------------------------------------ |
|      | `aria-label=Breadcrumb` | `nav`   | Provides a label that describes the type of navigation provided in the `nav` element. |
|      | `aria-current=page`     | `a`     | Applied to the last link in the set to indicate that it represents the current page. |

## Attention
1. Do not use string `/` as separators
2. add `aria-current=page` to the last link ( last link )

## Example
[Breadcrumb Accessibility Example Website](https://www.w3.org/TR/wai-aria-practices-1.1/examples/breadcrumb/index.html)

### html

```
<nav aria-label="Breadcrumb" class="breadcrumb">
  <ol>
    <li>
      <a href="../../">
        WAI-ARIA Authoring Practices 1.1
      </a>
    </li>
    <li>
      <a href="../../#aria_ex">
        Design Patterns
      </a>
    </li>
    <li>
      <a href="../../#breadcrumb">
        Breadcrumb Pattern
      </a>
    </li>
    <li>
      <a href="./index.html" aria-current="page">
        Breadcrumb Example
      </a>
    </li>
  </ol>
</nav>
```

### css

```
nav.breadcrumb {
  padding: 0.8em 1em;
  border: 1px solid hsl(0, 0%, 90%);
  border-radius: 4px;
  background: hsl(300, 14%, 97%);
}

nav.breadcrumb ol {
  margin: 0;
  padding-left: 0;
  list-style: none;
}

nav.breadcrumb li {
  display: inline;
}

nav.breadcrumb li + li::before {
  display: inline-block;
  margin: 0 0.25em;
  transform: rotate(15deg);
  border-right: 0.1em solid currentColor;
  height: 0.8em;
  content: "";
}

nav.breadcrumb [aria-current="page"] {
  color: #000;
  font-weight: 700;
  text-decoration: none;
}
```