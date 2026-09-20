# Passing a State Setter from Parent to Child

## Context

While building a dropdown in my React project, I wanted to control the dropdown state from a child component.

The state was defined in the parent:

```tsx
const [isOpen, setIsOpen] = useState(false);
```

I needed to pass `setIsOpen` to the child component.

## Problem

I wasn't sure what TypeScript type I should use for the `setIsOpen` prop.

## Solution

The correct type is:

```tsx
React.Dispatch<React.SetStateAction<boolean>>
```

For example:

```tsx
type Props = {
  setIsOpen: React.Dispatch<React.SetStateAction<boolean>>;
};

function Child({ setIsOpen }: Props) {
  return (
    <button onClick={() => setIsOpen(true)}>
      Open
    </button>
  );
}
```

Then I can pass the setter from the parent:

```tsx
<Child setIsOpen={setIsOpen} />
```

## What does this type mean?

A `useState` setter can receive either:

* A new value
* A function that receives the previous state

For example:

```tsx
setIsOpen(true);

setIsOpen(prev => !prev);
```

That's why the type is:

```tsx
React.Dispatch<React.SetStateAction<boolean>>
```

In simple terms, it means:

> This prop is a React state setter that can update a `boolean` state.

## General Pattern

The same pattern works with other state types:

```tsx
useState<boolean>
→ React.Dispatch<React.SetStateAction<boolean>>

useState<string>
→ React.Dispatch<React.SetStateAction<string>>

useState<number>
→ React.Dispatch<React.SetStateAction<number>>
```

## What I Learned

I learned that when passing a `useState` setter to another component, I can type it with:

```tsx
React.Dispatch<React.SetStateAction<T>>
```

where `T` is the type of the state.

Another small lesson from building my project.
