# Blog on Typescript

## Differences between interfaces and types in TypeScript

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
```

**Type:**
Unlike an interface, the type alias can also be used for other types such as primitives, unions, and tuples.

```ts
// primitive
type Name = string;

// object
type PartialPointX = { x: number; };
type PartialPointY = { y: number; };

// union
type PartialPoint = PartialPointX | PartialPointY;

// tuple
type Data = [number, string];
```

```ts
type Person = {
  name: string;
  age: number;
};
```

## 🔍 Feature Comparison: Type vs Interface in TypeScript

| **Feature**                                 | **Type**                                                                 | **Interface**                                                             |
|---------------------------------------------|--------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Definition**                              | A collection of data types.                                              | A syntactical contract.                                                  |
| **Flexibility**                             | More flexible.                                                           | Less flexible compared to `type`.                                        |
| **Keyword**                                 | Uses the `type` keyword.                                                 | Uses the `interface` keyword.                                            |
| **Naming**                                  | Supports creating a new name for a type.                                 | Provides a way to define entities.                                       |
| **Capabilities**                            | Has fewer capabilities.                                                  | Has more capabilities.                                                   |
| **Object Usage**                            | Does not inherently support object-based extension.                      | Supports the use and extension of objects.                               |
| **Merged Declarations**                     | Does not support multiple merged declarations.                         | Supports multiple merged declarations.                                |
| **Name Conflicts**                          | Two types with the same name raise an exception.                       | Two interfaces with the same name get merged.                         |
| **Implementation in Classes**               | Not used for implementation purposes.                                    | Used for implementation and extension in classes.                        |
| **Union Types**                             | Can define union types.                                                | Cannot implement or extend union types.                               |
| **Intersection Types**                      | Can create intersection types.                                         | Cannot create intersection interfaces.                                |
| **Usage with Primitives, Unions, Tuples**   | Can define primitives, unions, and tuples.                             | Cannot be used for these types of declarations.                       |



# Interface using extends:

## Difference between any, unknown, and never types in TypeScript
