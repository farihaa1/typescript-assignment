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

**Type:**

```ts
type Person = {
  name: string;
  age: number;
};


## Difference between any, unknown, and never types in TypeScript

