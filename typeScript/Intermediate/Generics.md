```javascript
function add(num1:number|string,num2:number|string):number|string{
    if(typeof num1 === "string" || typeof num2 ==="string"){
        return num1+""+num2;
    }
    return num1 + num2;
};
console.log(add(2,"Hai"));
```
output:- 
```
2Hai
```
This is a way of writing a function which can accept different dataTypes, but if got a lot of dataTypes this is not a good way!
### To avoid this issue we can use Function overloading.

```javascript
function addMe(num1:number , num2:number):number;
function addMe(num1:string , num2:string):string;
function addMe(num1:any,num2:any):any{
    return num1 + num2;
};
console.log("AddMe:",addMe("R1","5"));
```
output:- 
```
"AddMe:",  "R15" 
```

Which is also not that better way!(May we need to write a lot of overloading unwantedly).

### Here comes the GENERICS to picture.
Syntax:-
```javascript
//generics
function getAge<T>(age:T):T{
    return age;
}

getAge<string>("Ten");
```
eg:-
```typescript
function getDetails<T>(detail:T):T{
    return detail;
}


type UserDetails={
    name:string;
    age:number
}
type AdminDetail=UserDetails&{  //instead of writing the key values of userDetails again,!i merged it withadminDetails.
    role:string;
    need:boolean;
}
const customUserDetail: UserDetails ={
    name: "yadhu",
    age:23
}
const customAdminDetail: AdminDetail ={
    name: "yadhu",
    age:23,
    role:"Guest",
    need: true
}





console.log("detail1:",getDetails<UserDetails>(customUserDetail));
console.log("detail2",getDetails<UserDetails>(customAdminDetail));


```

output:-

```
[LOG]: "detail1:",  {
  "name": "yadhu",
  "age": 23
} 
[LOG]: "detail2",  {
  "name": "yadhu",
  "age": 23,
  "role": "Guest",
  "need": true
} 
```
in the detail2 I added ExtraValues in the customAdminDetail ( role:"Guest",need: true ) but the UserDetail type only have name and age.
 Even though it returns, full customAdmin values. why?

### TypeScript allows this — why?
Because TypeScript uses structural typing (or duck typing).

If it looks like a UserDetails, it's allowed to be treated like one — even if it has extra stuff.

`Think of it like this:`
```
🧸 You ask for a box with 2 toys: a car and a ball.
Someone gives you a box with 3 toys: car, ball, and a robot.
You're still happy — because the box has what you asked for!
```
That’s why this works:
```ts
getDetails<UserDetails>(adminDetail)
```

if we are using interface instead of types:-
```ts
interface UserDetails{
    name:string;
    age:number
}
interface AdminDetail extends UserDetails{//instead of writing the key values of userDetails again,!i merged it withadminDetails.
    role:string;
    need:boolean;
}
const customUserDetail: UserDetails ={
    name: "yadhu",
    age:23
}
const customAdminDetail: AdminDetail ={
    name: "yadhu",
    age:23,
    role:"Guest",
    need: true
}
```
