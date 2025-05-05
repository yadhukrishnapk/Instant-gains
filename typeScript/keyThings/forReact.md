

## ⚛️ 10. TypeScript in React

---

### 🔡 Typing Props

**Component Props:**

```ts
type UserProps = {
  name: string;
  age: number;
};

const UserCard: React.FC<UserProps> = ({ name, age }) => (
  <div>{name} is {age} years old.</div>
);
```

💡 `React.FC` automatically types `children` too!

---

### 🧠 Typing State (`useState`)

```ts
const [count, setCount] = useState<number>(0);
const [user, setUser] = useState<User | null>(null);
```

> Tip: Always use `null` or `undefined` if the value might not be set at first.

---

### 🎣 Typing Refs (`useRef`)

```ts
const inputRef = useRef<HTMLInputElement>(null);

useEffect(() => {
  inputRef.current?.focus(); // Safe access with optional chaining
}, []);
```

---

### 🖱️ Typing Events

```ts
const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
  console.log(e.target.value);
};
```

Other examples:

* `MouseEvent<HTMLButtonElement>`
* `FormEvent<HTMLFormElement>`

---

## 🤯 Common Confusing Doubts for React Devs Switching to TypeScript

---

### ❓ 1. **Do I need to type everything?**

**Answer:** No! TypeScript can infer types in many cases. Only type explicitly when:

* Passing props
* Managing complex state
* Using `useRef`, `useReducer`, or `useContext`

---

### ❓ 2. **Why does `useState` sometimes need a type?**

**Answer:** If the initial value doesn't make the type obvious (like `null` or `[]`), TS can't infer it. You must help:

```ts
const [data, setData] = useState<string[] | null>(null);
```

---

### ❓ 3. **Why does `useRef(null)` throw a type error?**

**Answer:** `null` has no type. You need to **pass a generic**:

```ts
const inputRef = useRef<HTMLInputElement>(null);
```

---

### ❓ 4. **How do I type optional props?**

**Answer:** Add a `?`:

```ts
type Props = { name?: string };
```

---

### ❓ 5. **How do I type children?**

**Answer:**

* If you're using `React.FC`, it already includes `children`.
* If not:

```ts
type Props = { children: React.ReactNode };
```

---

### ❓ 6. **Why does my `map()` give an error?**

**Answer:** Usually your array isn’t properly typed. Fix it like:

```ts
const users: User[] = [{ name: "A", age: 22 }];
users.map((user) => <p>{user.name}</p>);
```

---

### ❓ 7. **How do I type an event for form or input?**

**Answer:**

```ts
(e: React.ChangeEvent<HTMLInputElement>)
```

For form submit:

```ts
(e: React.FormEvent<HTMLFormElement>)
```

---

### ❓ 8. **How do I type context values?**

**Answer:** Create a context type and pass it in:

```ts
type Theme = "light" | "dark";

const ThemeContext = React.createContext<Theme>("light");
```

---

### ❓ 9. **How do I type a component with generics (like a dropdown)?**

```ts
type Option<T> = {
  label: string;
  value: T;
};

function Dropdown<T>({ options }: { options: Option<T>[] }) {
  return <select>{options.map(o => <option>{o.label}</option>)}</select>;
}
```

---

### 🎁 Bonus Tip: Default to being strict!

Set your `tsconfig.json` to `"strict": true` for the best protection — it will guide you.

---



# React.FC in TypeScript: Benefits and Best Practices

React.FC (Function Component) is a TypeScript type that was introduced to help with typing React functional components. Let me explain when to use it, its benefits, and current best practices.

## Benefits of React.FC

1. **Implicit children prop typing** - React.FC automatically includes the children prop in its type definition
2. **Type checking for props** - Ensures your component receives correctly typed props
3. **Better IDE autocompletion** - Can improve development experience with better suggestions
4. **Explicit declaration** - Makes it clear that a function is intended to be a React component

## When NOT to use React.FC

1. **Modern React doesn't require it** - The React team and community have moved away from recommending it
2. **Children typing limitations** - The implicit children type isn't always what you want
3. **Default props handling** - Has issues with how it handles defaultProps
4. **Extra verbosity** - Adds syntax without providing significant benefits in modern TypeScript

## Current Best Practice

The current best practice (as of May 2025) is to **not use React.FC** and instead use explicit function declarations with proper prop typing:

```typescript
// Instead of:
const MyComponent: React.FC<Props> = ({ name }) => {
  return <div>Hello {name}</div>;
};

// Use:
interface Props {
  name: string;
  children?: React.ReactNode; // Explicitly type children when needed
}

function MyComponent({ name, children }: Props) {
  return <div>Hello {name}{children}</div>;
}
```

The React team has been moving away from React.FC since around 2020, and this approach offers better flexibility with TypeScript's improved type inference.

## Key Reasons for the Shift Away From React.FC

1. React's TypeScript definitions have improved significantly
2. The explicit approach gives you more control over children typing
3. Better compatibility with newer React patterns and hooks
4. Improved type inference in modern TypeScript versions

