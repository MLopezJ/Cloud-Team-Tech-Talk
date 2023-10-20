# `any` vrs `unknown` in TypeScript

> Conversation started in this PR: [86e3a66b806d11d63f8871b29465940eca7b5374](https://github.com/MLopezJ/asset-tracker-lwm2m-js/pull/16/commits/86e3a66b806d11d63f8871b29465940eca7b5374)

## Agenda

- Technical definition
- Analogy
- When to use any
- When to use unknown
- Conclusion

## Technical definition

### Any

It is a dynamic type that represents a value of any data type.

```ts
let myVariable: any;
myVariable = 10; // Valid, myVariable can hold a number
myVariable = "Hello, TypeScript!"; // Valid, myVariable can hold a string
myVariable = true; // Valid, myVariable can hold a boolean
```

The biggest implication of this type is that the compiler interpret it as an instruction for disable type checking in TypeScript. It is similar to put `@ts-ignore` comment around every usage of the variable. [+info](https://www.typescriptlang.org/docs/handbook/declaration-files/do-s-and-don-ts.html#any)

### Unknown

unknown is the type-safe counterpart of any

```ts
let myVariable: unknown;
myVariable = 10; // Valid, but TypeScript considers it of type unknown

// Error: Object is of type 'unknown'.
console.log(myVariable.toFixed(2));

// To use it, you need to narrow down the type:
if (typeof myVariable === "number") {
  // Now TypeScript knows that myVariable is a number
  console.log(myVariable.toFixed(2));
}
```

Anything is assignable to unknown, but unknown isn’t assignable to anything but itself and any without a type assertion or a control flow based narrowing. Likewise, no operations are permitted on an unknown without first asserting or narrowing to a more specific type. [+info](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-0.html#:~:text=unknown%20is%20the%20type%2Dsafe,to%20a%20more%20specific%20type)

## Analogy

If we think variable as a box for data storage, a type in TypeScript are guards checking if the data fits in that interface.

![Analogy](../img/DALL·E%202023-10-20%2014.07.02.png)
> Image generated with DALL·E. Prompt: Draw a box that represents a storage for binary data. This box has a big door in front of it.  And in front of the door, there are 4 guards of Buckingham Palace protecting the box. 

With `any` we are basically having the guard there but ordering them to do not check.

With `unknown` we are ordering guards to allow them to store everything but check everytime data from that box is planning to be used.

## When to use `any`

When you are in the process of migrating a JavaScript project to TypeScript. `any` can be used as type for for stuff you haven’t migrated yet.

## When to use `unknown`

When you do not know the type of that variable at that moment but you will be interested in using TypeScript check benefits when the variable is benign used.

## Conclusions

- If you are using `any` several times in your TypeScript project you would ask yourself if you really need TypeScript.

- `any` disable TypeScript type checking. Proceed with caution when used.

- `unknown` accept all type on assignation and does type checking when the variable is benign used.
