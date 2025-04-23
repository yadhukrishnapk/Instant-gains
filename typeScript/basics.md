## infer types
```javascript
let userName:string = "wow";
let counts:number =30000;
let isSubscribed: boolean = true;
let skills:string[]=["js","css","ts"];
let countArray: number[]=[1,2,3,4];
let emptyArray:[]=[];
let userDetails:{name:string;age:number;salary:number}={
    name:"yadhu",
    age:99,
    salary:300000
}
```

## interface
```javascript
interface Details{
    name:string;
    age:number;
    salary:number;
    getName:()=>void;
}
let userDetails:Details={
    name:"Yadhu",
    salary:99_0000,
    age:32,
    getName(){
        console.log("hey")
    }
}
let adminDetails:Details={
    name:"Yadhu",
    salary:99_0000,
    age:32,
    getName(){
        console.log("admin")
    }
}
```
interface is always in the form of objects

## type
```javascript
type address={
    place:string;
    area:string;
    streeNo:number;
}

let myAddress:address={
    area:"kty",
    place:"ckdy",
    streeNo:87
}
```
## union(we can use it in interface also)

```javascript
type Work={
    workName:string;
    salary:number | string;
}
let yadhusWork:Work={
    salary:8900,
    workName:"developer"
}  

```

## optional

```javascript
type Party={
    area:string;
    liquor?:boolean
}

let yadhusParty:Party={
    area:"koratty",
    // liquor:false
}

/////functions
function userWork(userDetails:Work){
    return userDetails.salary
}
userWork(yadhusWork)
```
## named types
```javascript
 type Status = "pending" | "completed" | "failed";
// type myStatus ={
//     name : string,
//     mood :string,
// }
// type Status1=string;
// // interface is always in the form of objects

let currentStatus: StatusType = "";
const response = "pending";
if(response === "pending"){
    currentStatus="pending"
}
```


# TypeScript Type System Overview


## 1. Implicit Types vs Explicit Types

**Implicit Types (Type Inference)**:
- TypeScript automatically figures out the type based on the value assigned
- You don't need to write the type yourself
- Example: `let name = "John"` (TypeScript infers this as a string)

**Explicit Types**:
- You specifically tell TypeScript what type to use
- Uses a colon followed by the type
- Example: `let name: string = "John"`

## 2. Any Type

The `any` type allows a variable to hold values of any type:
```typescript
let data: any = 42;
data = "hello";  // No error
data = true;     // No error
data = [1, 2, 3]; // No error
```

It's essentially an escape hatch from TypeScript's type checking.

## 3. Losing Type Safety with Any

When you use `any`, you lose TypeScript's benefits:
- No IntelliSense/autocomplete
- No compile-time error checking
- Can lead to runtime errors
- Defeats the purpose of using TypeScript

Example of problem:
```typescript
let userData: any = { firstName: "John" };
console.log(userData.lastName.toUpperCase()); // No TypeScript error, but runtime error!
```

## 4. Unknown Type

A safer alternative to `any`:
- Can hold any value, like `any`
- But you must check the type before performing operations
- Forces you to verify type before using it

```typescript
let userInput: unknown = "Hello";

// This won't work:
// console.log(userInput.length); // Error!

// You must check the type first:
if (typeof userInput === "string") {
  console.log(userInput.length); // Works fine
}
```

## 5. Never Type

In TypeScript, never is a type that represents values which never occur. It's used primarily in scenarios where a function will never return a value, either because it always throws an error or it runs indefinitely. The never type is assignable to every other type, but no type, except never itself, is assignable to never. 

Represents values that never occur:
- Functions that always throw errors
- Functions with infinite loops
- Impossible conditions

```typescript
function throwError(message: string): never {
  throw new Error(message);
}

function infiniteLoop(): never {
  while (true) {
    // do something forever
  }
}
```

## 6. Enum

Enums define a set of named constants:
- Helps with readability
- Creates a namespace of related values

```typescript
enum Direction {
  North,
  East,
  South,
  West
}

let myDirection: Direction = Direction.North;

// By default, enums are number-based starting from 0
console.log(myDirection); // 0

// You can set custom values:
enum HttpStatus {
  OK = 200,
  NotFound = 404,
  ServerError = 500
}
```

## 7. Tuple

Fixed-length arrays where each position has a specific type:
- Stricter than regular arrays
- Order matters
- Length is fixed

```typescript
// Define a tuple
let person: [string, number, boolean] = ["John", 30, true];

// Accessing elements with correct type
let name: string = person[0];
let age: number = person[1];
let isActive: boolean = person[2];

// Error: Type 'number' is not assignable to type 'string'
// person[0] = 42;
```

## 8. Objects

TypeScript allows you to define object shapes with interfaces or type aliases:

```typescript
// Using interface
interface User {
  name: string;
  age: number;
  active?: boolean; // Optional property
  readonly id: number; // Can't be changed after creation
}

// Using type alias
type Product = {
  title: string;
  price: number;
  inStock: boolean;
};

// Using an object type
let customer: { id: number; name: string } = {
  id: 1,
  name: "Alice"
};

// With excess property checking
// This would cause an error:
// let wrongCustomer: { id: number } = { id: 2, name: "Bob" };
```

Object types can be nested, combined, and extended in various ways to model complex data structures.
