# Null priority bug and contorl it between the Zod & UI & action
## Context 
When I created a Task that it had only title, then I clicked on edit task and add others subjects in the Task ,just Priority feature was empty , there was an error 
```tsx
there is nothing task 
```
## Problem 
When I create a Task without priority , so makes a `Null` value in database then when I want to edit the Task and don't put the value on priority element so it makes the
Error.
because I write this code on Schema file : 
```tsx
priority: z.preprocess(
    (value) => (value === undefined ? "" : value),
    z.enum(["LOW", "MEDIUM", "HIGH", "URGENT"]).optional(),
  ),
  ```
  ## What I tried 
  At first I thought the problem is on the first part of the condition in Schema so I changed `undefinde` to `""` .
  but it didn't work
  ## Solution
  The solution was control `null` in all part of the project. so I ckecked the SchemaEdit file and find it finaly.
  I must changed `undefind` to `null` in that code
  ```tsx
priority: z.preprocess(
    (value) => (value === null ? "" : value),
    z.enum(["LOW", "MEDIUM", "HIGH", "URGENT"]).optional(),
  ),
   ```
   ## What I learned
   I learned checked the error and control all values in UI , Database , Schema.
