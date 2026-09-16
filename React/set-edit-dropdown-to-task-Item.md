# How I put edit task feature into every of the Todo
## Context 
While working on FocusYar, I wanted to put drop down edit task on the any of the Todos.
## problem
I had the clicked on the Todo and opened edit task drop down, some of it was hidden in to task item.
## What I tried 
at first I tried : 
i change overFollow-y-auto place.
but it didn't work 

## solution
At first we need to know position of the edit Todo icon so we should use : 
### getBoundingClientRect()
we need to a state to control and set position of edit icon.
```tsx
const [editPosition, setEditPosition] = useState({
    top: 0,
    left: 0,
  });
```
then we add `editPosition` to handelFunction our subject and seti it values by getBoundingClientRect() values,

```tsx
function handleEdit(
    id: number,
    event: React.MouseEvent<HTMLDivElement>
  ) {
    const rect = event.currentTarget.getBoundingClientRect();

    setEditPosition({
      top: rect.top,
      left: rect.left,
    });
    setIsEditTaskOpen(id);
  }
```
well we got the position right now, then we should put the drop down edit in the appropriate position and out of the Todo place.
then we must put this code in to it : 
```tsx
 style={{
    top: editPosition.top + 25,
    left: editPosition.left + 10,
 }}
```

## What I learned
I learn how does `getBoundingClientRect()` work, and I can set any thing by it also I learned `z-index` didn't work anywhere.
