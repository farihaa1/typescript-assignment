# Blog on Typescript

## Differences Between `interface` and `type` in TypeScript

In TypeScript, both interface and type are used to define the structure of objects, but they differ in flexibility and usage. While interface is extendable and primarily for object shapes, type is more versatile, allowing unions, intersections, and more complex type definitions.

---

## Interface vs Type

### Syntax

**Interface:**
Interfaces define a standard structure that implementing classes must follow. It is the virtual structure that is used for type-checking.

```ts
interface Person {
  name: string;
  age: number;
}

// Can extend other interfaces
interface Employee extends Person {
  salary: number;
}
```

**Type:**
Unlike an interface, the type alias can also be used for other types such as primitives, unions, and tuples.

```ts
type Person = {
  name: string;
  age: number;
};
```

```ts
// primitive
type Name = string;

// object
type PartialPointX = { x: number };
type PartialPointY = { y: number };

// union
type PartialPoint = PartialPointX | PartialPointY;

// tuple
type Data = [number, string];
```

## 🔍 Feature Comparison: Type vs Interface in TypeScript

| **Feature**                               | **Type**                                               | **Interface**                                     |
| ----------------------------------------- | ------------------------------------------------------ | ------------------------------------------------- |
| **Definition**                            | A way to name any type (object, union, function, etc.) | A rule-book for how an object should look         |
| **Flexibility**                           | More flexible.                                         | Less flexible compared to `type`.                 |
| **Keyword**                               | Uses the `type` keyword.                               | Uses the `interface` keyword.                     |
| **Naming**                                | Supports creating a new name for a type.               | Provides a way to define entities.                |
| **Capabilities**                          | Has fewer capabilities.                                | Has more capabilities.                            |
| **Object Usage**                          | Does not inherently support object-based extension.    | Supports the use and extension of objects.        |
| **Merged Declarations**                   | Does not support multiple merged declarations.         | Supports multiple merged declarations.            |
| **Name Conflicts**                        | Two types with the same name raise an exception.       | Two interfaces with the same name get merged.     |
| **Implementation in Classes**             | Not used for implementation purposes.                  | Used for implementation and extension in classes. |
| **Union Types**                           | Can define union types.                                | Cannot implement or extend union types.           |
| **Intersection Types**                    | Can create intersection types.                         | Cannot create intersection interfaces.            |
| **Usage with Primitives, Unions, Tuples** | Can define primitives, unions, and tuples.             | Cannot be used for these types of declarations.   |

**When to Use What?**

1.Use interface when working with object shapes, OOP-style code, or you want to take advantage of declaration merging.

2.Use type when you need unions, tuples, intersections, or aliasing primitives and functions.

## Difference between any, unknown, and never types in TypeScript

TypeScript introduces advanced types that allow for better type safety and flexibility. Among these, `any`, `unknown`, and `never` types have specific roles and behaviors that can sometimes be confusing. In this blog, we’ll explore each of them and clarify their differences, best-use scenarios, and how they improve code quality.

---

## `any` Type

### What is `any`?

The `any` type in TypeScript is a wildcard that disables type checking for a variable. It tells TypeScript to essentially “turn off” static type checking for that variable, which can be useful when you're unsure of the type or working with dynamically typed data.

However, using `any` sacrifices type safety, making your code more prone to errors.

```ts
let anything: any = 5;
anything = "hello";
anything = true;
```

When to use any?

1.When integrating with third-party JavaScript libraries that don’t have type definitions.
2.When you're migrating from JavaScript to TypeScript and need a temporary solution.
3.For quick prototyping, where you’re willing to sacrifice type safety for flexibility.

⚠️ Caution: Overusing any defeats the purpose of using TypeScript, which is to gain strong typing and safety.

## `unknown` Type

### What is `unknown`?

The unknown type is similar to any, but with a crucial difference: TypeScript will not allow operations on a value of type unknown without first asserting or checking the type. This adds an additional layer of safety compared to any.

```ts
let value: unknown = "hello";

// Error! TypeScript won't allow you to access properties on `unknown` type.
console.log(value.length); // Property 'length' does not exist on type 'unknown'.

// Correct approach: Type assertion or type guard
if (typeof value === "string") {
  console.log(value.length); // Okay now that TypeScript knows it's a string
}
```

### When to use `unknown`?

1. When you want to enforce type checks before performing operations on a variable.
2. If you’re working with data of uncertain type, such as from APIs or external sources.
3. Use it when type safety is more important than flexibility.

🧠 Pro Tip: Use unknown over any when you want safe handling of dynamically typed data.

**never Type**

### What is `never`?

The never type represents values that will never occur. It's typically used in cases where you expect an impossible situation, such as when a function throws an error or enters an infinite loop.

A common use of never is in functions that never return a value.

```ts
function throwError(message: string): never {
  throw new Error(message);
}

function infiniteLoop(): never {
  while (true) {
    // Infinite loop
  }
}
```

### When to use `never`?

1.When a function always throws an error or doesn’t complete its execution.
2.In exhaustive checks, such as when dealing with union types in switch statements to ensure all cases are handled.

⚠️ Caution: You should not assign never to a variable because it represents an impossible value.

## Features Comparison: `any`, `unknown`, and `never` Types in TypeScript

| **Feature**                             | **`any`**                                      | **`unknown`**                                 | **`never`**                                    |
|-----------------------------------------|------------------------------------------------|-----------------------------------------------|------------------------------------------------|
| **Type Safety**                         | `any` provides no type safety. You can assign any value to it, which makes it flexible but also prone to errors. | `unknown` is safer than `any`. You must check the type before using it. This adds an extra layer of protection. | `never` is used for functions or values that can never return a valid result (e.g., throwing an error or infinite loops). It’s guaranteed to never happen. |
| **Use Case**                            | Use `any` when working with data that can vary widely, like when you’re integrating with third-party libraries or APIs. It’s also useful in quick prototyping. | Use `unknown` when you need to handle dynamic data, but you want to enforce some safety by making sure the data is the right type before using it. | `never` is used for functions that either always throw an error or never finish (like an infinite loop). It’s for situations where something logically can’t happen. |
| **Assignable to Other Types**           | With `any`, you can assign it to any other type without any restrictions. | `unknown` can’t be used directly without checking its type first. You must validate it before performing any operations. | You can’t assign a `never` type to any other variable since it represents an unreachable or non-returning type. |
| **Operations Allowed**                  | With `any`, you can perform any operation, which can be risky since TypeScript won’t catch potential errors. | With `unknown`, TypeScript won’t let you perform operations until you check what type the value is. This ensures safety. | You can’t perform any operations with `never`. It's used for cases where you have dead-end code, like errors or infinite loops. |
| **Typical Usage**                       | Use `any` when you're not sure about the type of data, need flexibility, or when transitioning from JavaScript. | Use `unknown` when you’re handling dynamic or uncertain data but still want to enforce type safety by checking the type first. | Use `never` for functions that either don’t return a value (like throwing errors) or have an infinite loop. |



**_Final Thoughts_**

any provides maximum flexibility but sacrifices type safety, making it useful in quick-and-dirty situations or integrating external data.
unknown is a safer alternative to any, enforcing type checks before performing operations on unknown data.
never is used for functions or values that never return, representing unreachable code or errors.

