# ListBox
A listbox widget presents a list of options and allows a user to select one or more of them. A listbox that allows a single option to be chosen is a single-select listbox; one that allows multiple options to be selected is a multi-select listbox.

## Attention
1. When screen readers present a listbox, they may render the name, state, and position of each option in the list 
2. The name of an option is a string calculated by the browser, typically from the content of the option element
3. If an option contains a semantic element, such as a heading, screen reader users will not have access to the semantics
4. The interaction model conveyed by the listbox role to assistive technologies does not support interacting with elements inside of an option
5. Avoiding very long option names facilitates understandability and perceivability for screen reader users
6. Avoiding sets of options where each option name starts with the same word or phrase because this will significantly degrade usability for keyboard and screen reader users