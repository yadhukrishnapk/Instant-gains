## Enums

```ts
enum StatusType{
    PENDING =1,
    COMPLETED,
    FAILED
}
function getStatus(orderID:string,status:StatusType){
    console.log(orderID,"==",status);
}
console.log(getStatus("123456",StatusType.COMPLETED))
```


Great! Since you're learning TypeScript, getting comfortable with `enum`s is a smart move. Let's break it down **simply** and explain:

---

## ✅ What is an `enum` in TypeScript?

An `enum` is a way to define a **set of named constants**. It makes your code more readable and **less error-prone** when working with fixed values.

---

## 🔧 When should you use `enum`?

Use enums when:

1. ✅ You have a fixed set of related values.
2. ✅ You want to **avoid magic strings** or hardcoded numbers.
3. ✅ You want to write safer and cleaner conditions/switches.

---

## 🔥 Common real-life use cases:

### 1. **User roles**
```ts
enum Role {
  Admin,
  User,
  Guest
}

const currentRole: Role = Role.Admin;
```

### 2. **Status values**
```ts
enum Status {
  Pending = "PENDING",
  Success = "SUCCESS",
  Failed = "FAILED"
}

function showStatus(status: Status) {
  if (status === Status.Success) {
    console.log("🎉 Success!");
  }
}
```

### 3. **Days, directions, or types**
```ts
enum Direction {
  Up,
  Down,
  Left,
  Right
}
```

---

## 👀 Things to Know About `enum`s:

### 1. **Numeric enums** (default)
```ts
enum Direction {
  Up,    // 0
  Down,  // 1
  Left,  // 2
  Right  // 3
}
```

### 2. **String enums**
```ts
enum Status {
  Success = "SUCCESS",
  Failed = "FAILED"
}
```

These are better for debugging (you’ll see readable names instead of numbers).

### 3. **Custom values**
```ts
enum HttpCode {
  OK = 200,
  NotFound = 404,
  ServerError = 500
}
```

---

## 🛡️ Why enums are useful?

✅ Prevent typos  
✅ Self-documenting  
✅ Type-safe  
✅ Better code suggestions (autocomplete)  
✅ Easier to change/update

---

## ⚠️ Enum vs Union Type?

Sometimes union types can do the job better (lighter and safer):

```ts
type Role = "admin" | "user" | "guest";

function check(role: Role) {
  if (role === "admin") console.log("Access granted");
}
```

### 👍 Use union types when:
- You don't need complex mapping or reverse lookup.
- You just need simple string options.

---

## TL;DR - When to use `enum`

| Situation | Use Enum? |
|----------|-----------|
| Fixed set of values with logic or mapping | ✅ Yes |
| Simple strings with no mapping | ❌ Use union type |
| Need readable constants | ✅ Yes |
| Need reverse lookup | ✅ Yes |
| Need tree-shaking in modern frontend apps | ❌ Prefer `as const` object or union type |

---

Let me know if you want a cheat sheet or visual version of this. I can also show how enums behave in JavaScript output if you're curious!
