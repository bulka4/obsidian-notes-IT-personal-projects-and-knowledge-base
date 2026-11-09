Tags: [[__Frontend_engineering]] [[_React]]
#Frontend #React 

# Introduction
When creating a React element ([[React - Components and elements|link]]), we can always provide the `key` attribute:
```typescript
<Component
    key={id}
    arg1={value1}
/>
```

It is metadata used internally by React to track elements across renders, particularly when rendering lists.

React uses `key` internally when reconciling the component tree (comparing the previous and new versions of the UI).

For example, suppose the initial list is:
```
Task 1 (key=1)
Task 2 (key=2)
Task 3 (key=3)
```

Then we remove Task 2.

React receives a new list:
```
Task 1 (key=1)
Task 3 (key=3)
```

React can identify that:
- Task 1 is still the same element.
- Task 2 was removed.
- Task 3 is still the same element.

This helps React update the UI correctly without unnecessarily recreating elements.

Importantly, keys help React preserve component identity and state when items move, are added, or are removed.
# `React.Attributes`
`React.Attributes` is a TypeScript interface provided by React's type definitions.

It defines special attributes that React accepts when creating elements.

Its simplified definition looks like this:
```typescript
interface Attributes {
    key?: string | number | null;
}
```

The `?` means the attribute is optional.
# Important rules for using `key` and facts
- Keys should be unique among sibling elements.
- Avoid array indexes as keys if elements can be added, removed, or reordered (because if we do this, then the same element can get a different key value, e.g. after removing an element and re-rendering)
- Keys are used by React, not rendered as HTML attributes