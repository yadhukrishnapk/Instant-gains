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
