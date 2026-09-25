# Using a Discriminated Union for Action Results

## Problem

I tried using `undefined` in the schema and also changed the Action's `data` type:

```ts
data: unknown | undefined
```

But the problem remained.

## Solution

The actual issue was the return type of the Action.

I defined a discriminated union:

```ts
type ReadTasksResult =
  | {
      success: true;
      todo: Todo;
    }
  | {
      success: false;
      message: string;
      error?: Record<string, string[] | undefined>;
    };
```

Now TypeScript can narrow the result using `success`:

```ts
if (result.success) {
  console.log(result.todo.title);
}
```

## Key takeaway

A discriminated union can clearly represent different states of an Action result and allows TypeScript to safely narrow the type.
