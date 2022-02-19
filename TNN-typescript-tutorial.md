# TypeScript tutorial (The Net Ninja)

[link to playlist](https://www.youtube.com/watch?v=2pZmKW9-I_k&list=PL4cUxeGkcC9gUgr39Q_yD6v-bSyMwKPUI)

[TypeScript docs](https://www.typescriptlang.org/docs/)

## 1 - Intro & setup

TypeScript is a programming language that is an alternative to JS. It is a superset of JavaScript- meaning it extends it with new feature and syntax. It can do all the things JS can do, but more stuff as well. 

Browsers do not understand typescript by default. TS must be compiled into JS in order to be understood. In most cases, the extra step to compile is very easy.

### Some useful features of TS: 

1. Allows us to use **strict types**: if we declare a variable to be a certain type (ex. a number), we then cannot change the type in that variable to a string, boolean, etc. This makes error checking and debugging easier. 

In contrast, JS uses **dynamic types**, where variables can change at any point. This can introduce errors more easily. 

2. TS supports modern features of JS (let, const, arrow func, etc.) that may not be fully supported yet in browsers. During compilation, it will be turner into older JS that all browsers can understand. 


## 2 - Compiling Typescript

### Installing the TypeScript compiler

Open a terminal window and `npm install -g typescript`


In the mini project folder (TNN-TS-app), there is a `sandbox.js` file- but we want to create a new file called `sandbox.ts`.

Some test code in the TS file:

```
const character = 'mario';
console.log(character);
```

If we check the browser console, nothing will show up because: 

1. The index.html file is linking `sandbox.js` and not `sandbox.ts`
2. Even if the TS file was linked, it wouldn't work because the browser doesn't understand TS. 

Even if the code we wrote looks exactly the same as JS, it's a TS file so it still needs to be compiled. 

To compile it, open a terminal window in the same directory as the TS file, and type: 

`tsc sandbox.ts sandbox.js`

This means "compile the first file and put it into the second file".

There is a shortcut we can use if the name of the file before the extension is the same for the TS and JS files:

`tsc sandbox.ts`

This automatically compiles the code to a file with the same name but with the JS extension. 

If we check the compiled code in the JS file, we can see that it has changed `const` into `var`. The console log also now shows up in the browser. 

However, there is now an error popping up in the TS file: `cannot re-declare block-scoped variable 'character'`. This is just happening if both the TS and JS files are open at the same time. If we close one file, the error will go away. 

For now, every time we change the TS file, we need to manually recomiple it to the JS file. We would rather watch for the file constantly and only run the command once- to do this we can run: 

`tsc sandbox.ts -w` which watches for changes in the file and compiles automatically. 


## 3 - Type basics

The main difference between TS and JS is that TS uses strict types- if we declare a variable in TS as a string for example, it will always be a string and its type cannot change later. 

The way we declare a variable is exactly the same as we would in a JS file. 

```
let character = 'mario';
let age = 30;
let isRetired = false;
```

TS only has one **number** type for integers, decimals and float, like JS. If we try to set the `character` to a different data type like so: 

```
character = 20;
```

We get an error: `type number is not assignable to type string`. It is not letting us change the type. We can still change the variable to another string, but not any other data type. 

Note that we don't need to `explicitly` state that character should be a string - TS infers that it should be a string based on the first value we assign it to. 


We can also declare what type of variable we expect to be passed to a function as an argument. We can use regular or arrow functions in TS. 


let's create a dummy function: 

```
const circ = (diameter) => {
  return diameter * Math.PI;
};
```

At the moment, we could pass any value to this function regardless of the type, without errors. 


If we pass in a string: 

`console.log(circ('hello'))`

There will be no compilation errors from TS, but in the console, we can see that it returns `NaN`. In TS, we can define the expected type of an argument when we declare the function by using the folowing syntax:

```
const circ = (diameter: number) => {
  return diameter * Math.PI;
};
```

Now, the code should no longer compile if we try to pass in the string like before, because it requires the argument to be a number. If we change the argument into a number, the code will compile again.


If we take a look at the JS file, the code doesn't actually seem different. This is because the code only compiles into the JS file if there are no errors in the TS files to begin with. 


## 4 - Arrays & objects

### Arrays in TypeScript

Here is an array of strings:
```
let names = ['luigi', 'mario', 'yoshi'];
```

We can push to the array a new string value with no issues:

`names.push('peach')`

However if we try to push a value that is not a string, it won't work. We can only add strings to this array- likewise if we try to change the value of an existing item using array indexing. 

If we wanted to have a mixed array with different types, we just have to include those types when we first declare the array:

```
let mixed = ['luigi', 30, true, 14];
```

Now we can add, or change values, into three types: string, number or boolean. Note that we can even change the type of a value in a certain position of the array, as long as the array expects that data type. For example if array[0] is initially a string, and the array was declared containing numbers as well, then array[0] can be changed into a number value.

**NOTE** When we declare an array in TS, we can't then reassign the entire array to a different type of value. For example: 


```
let names = ['luigi', 'mario'];

names = 'hello'
```


### Objects in TypeScript

```
let ninja = {
  name: 'mario',
  belt: 'black',
  age: 30
};
```

In the case of objects, if we declare a property to be a specific type, then it can only ever be that type. (As with arrays, the entire `ninja` object also cannot be redefined into another type such as a string).

```
ninja.age = 40  // OK
ninja.name = 'peach' // OK
ninja.age = 'hello'  // ERROR
```

We also cannot add on extra properties to the object after we first define them. 

`ninja.skills = ['fight', 'sneak']`

This will not work because the skills property did not exist on the ninja object to begin with. 


We can however, override the object with new values like this: 

```
ninja = {
  name: 'Yoshi',
  belt: 'green',
  age: 45
};
```

If we try to take out one of the properties when we override the object- for example if we remove the age property- there will be an error. It needs to match the structure of the object that we initially declared. 



## 5 - Explicit types & Union types

### Explicit types

Sometimes we want to initialise a variable without giving it a value, so TS can't infer its type. In this case, we can explicitly give the variable a type:

`let character: string;`

This basically means: initialise the character variable, don't give it a value yet but the value can only be a string in the future. 

What about in the case of arrays?

If we wanted an array of strings for example: 
`let myArray: string[];`

Note that the above line does not actually initialise the array with anything, so we would get an error if we tried to use methods like `push` on it. 

To initialise the empty array: `let myArray: string[] = []`
This is recommended over the previous line of code. 

### Union types

What if we want a mixed array with more than one type? In this case, we use a **union type**, which is basically a way to say that it could be one of several types.

```
let mixed: (string|number|boolean)[] = [];
```
We use the | symbol to mean OR. So in the example above, the array can contain either string, number or boolean types. 

Union types can also be used on variables that are not arrays. For example, we can declare an `id` variable that coule be either in string or number format: 

`let id: string|number`
Here, we don't need to use parantheses because we are not declaring an array. 


### Explicit type with objects

The simplest way to declare a variable as an object type is like this:

```
let ninjaOne = object;

ninjaOne = {
  name: 'Mario',
  age: 30
};

ninjaOne = [];  // THIS IS ALLOWED!
```

Note that we could even assign `ninjaOne` to be an array, since an array is a type of object in JS. 

However we could be more specific about the type of object we want a variable to be assigned. 

```
let ninjaTwo: {
  name: string,
  age: number
};
```

The above code says that ninjaTwo must be an object, and must have the specified properties inside it, with the specified types respectively. If we try to give it an array value, it won't work. 


## 6 - Dynamic (any) types

In TS, the **any** type is used to say that a variable can be any type, and can also change types in the future. 

```
let age: any;

age = 25;
```

Note that there is a shortcut to give the type and assign a value to the variable in one line like so: `let age: any = 25`

Even though age is given a number value, its type is still `any` as we can see when we hover over the variable. 

```
let age: any = 25;

age = 'hello';
age = { name: 'Bob' }; 
```

The code above is valid since age has a type of any. Note that this is essentially just using TS like normal JS, which defeats the purpose of using TS. There may be some rare cases where we would need to assign the **any** type, but we should be wary of using it. An example of when we could need this type is if we don't know what type a variable will have in the future.


### Any type with arrays and objects

The code below creates an empty array that can accept any type of value.

`let mixed: any[] = []`

Likewise for objects: 

`let ninja: {name: any, age: any}`



## 7 - Better workflow & tsconfig

Right now in our simple project we have only one sandbox.ts and one sandbox.js file. In a more complex project, there would be several TS and JS files, which would be separated into folders. 

A typical project organisation would be: 

- **Public folder** (index.html, compiled JS file, CSS)
- **src** (for source code that isn't deployed - such as the TS files)

However, if we now compile the TS file, it will generate a new JS file in the same folder as the TS file (src) which is not what we want. To get around this, we can initialise a `tsconfic.json` file in the root of the project: 

`tsc --init`

This file contains all the configuration options for TS. 

One of the options which is commented out by default, is the `rootDir` option. We will uncomment it and specify the src folder as the one containing the source code (TS). Also uncomment `outDir` and specify that the compiled code should go in the public folder:

```
"rootDir": "./src",
"outDir": "./public", 
```

Now if we want to watch all of our TS files in the project, we can simply run `tsc -w` in the root of the project. 

Not that creating a TS file outside the src folder will cause it to automatically compile the JS file in the public folder. To avoid this behavior, we can add something at the end of the `tsconfig` file: 

```
  },
 "include": ["src"]
}
```

This means "compile any TS files inside the src folder, but not anywhere else".



## 8 - Function type basics

In TS there is a **Function** type. 

```
let greet = () => {
  console.log('hello');
};
```

Here TS will automatically infer that `greet` has a type of function. As with other types, we can declare it as a Function type without automatically invoking it:

` let greet: Function;`
Note the capital F.


### Optional parameters & default values

Let's look again at the parameters we pass to a function:

```
const add = (a: number, b: number) => {
  return a + b;
};

add(2 + 5);  // 7

add(2);  // ERROR
```
The second example where we invoke this function, we get an error because we didn't pass in the second argument that was expected. In order to make an argument optional, we use the syntax: 

```
const add = (a: number, b: number, c?: number) => {
  return a + b + c;
};
```

The third paramater is optional in the example above. If we don't pass in the optional parameter, it becomes `undefined`. We can also specify a **default value** that an optional parameter should have if a number is not passed to it: 

```
const add = (a: number, b: number, c?: number = 10) => {
  return a + b;
};
```

Note that if we give a default value, we can remove the `?` syntax because even if nothing is passed in, it will use the default provided value. If a parameter is passed in, it overrides the default value. 

```
const add = (a: number, b: number, c: number = 10) => {
  return a + b + c;
};
```

We tend to not use both the `?` for optional parameters as well as providing a default value - just one or the other. 

As well, it's good practice to put any optional or default parameters **at the end** of the list of parameters. In other words required parameters should be listed as the first ones in the function:

`function(required, required, optional or default value)`


### types of return values


```
const add = (a: number, b: number) => {
  return a + b;
};

let result = add(2+7);
```

The `result` variable will automatically be given a number type. TS has inferred the type that is returned from the function. This means we cannot change the type of `result` in the future. 

We can also explicitly state the type of the return value when we declare the function:


```
const add = (a: number, b: number): number => {
  return a + b;
};
```
This is not really necessary, but can be useful if the function is large - we can see from the first line what type the function is supposed to return. 

What if a function doesn't return anything? For example, if the function just logs something to the console?

Technically, this kind of function still has a return value called **void**. Void represents a complete lack of return value, and turns into undefined when it is compiled into JS. However in TS, void is completely separate from undefined.


## 9 - Type aliases

Sometimes when working with functions that take parameters, and specifying the types of the parameters themselves, the code can get messy and hard to read:

For example:

```
const greet = (user: {name: string, id: string | number }) => {
  console.log(....etc);
};
```

We could also have more functions which uses exactly the same type specifications as another function - in which case we wouldn't want to repeat those specs. 

We can define our own **type aliases** at the start of the file, and then use them in whatever functions we need. 

```
type stringOrNum = string | number;

const greet = (user: {name: string, id: stringOrNum }) => {};
```
Likewise, we can specify the structure of an object: 

```
type userObject = {
  name: string, 
  id: stringOrNum
};

const greet = (user: userObject) => {};
```

This improves readability and reusability. 


## 10 - Function types (signatures)

We can be more specific when giving an explicit Function type to a variable, by assigning a **function signature**. The signature describes the general structure of a function- what arguments it takes in. and what type of data it returns.

For example, the signature: `() => void` means that the function takes no arguments and does not have a return value. 

### Example 1:

```
let greet: (a: string, b: string) => void;

greet = (name: string, greeting: string) => {
  console.log(`${name} says ${greeting}`);
}
```

Note that we can name the parameters (a & b) whatever we want. It doesn't have to match the names we give to the arguments of the function when we invoke it. However, the types of the arguments themselves must match. 


### Example 2:

```
let calc: (a: number, b: number, c: string) => number;

calc = (numOne: number, numTwo: number, action: string):number => {
  
  if (action === 'add') return numOne + numTwo;

  else return numOne - numTwo;
}
```


### Example 3:

```
let logDetails: (obj: { name: string, age: number }) => void;

logDetails = (ninja: {name: string, age: number}) => {
  console.log(`${ninja.name} is `${ninja.age}`);
}
```

We could use type aliases to make the code cleaner: 

```
let logDetails: (obj: { name: string, age: number }) => void;

type person = { name: string, age: number };

logDetails = (ninja: person) => {
  console.log(`${ninja.name} is `${ninja.age}`);
}
```


## 11 - The DOM and typecasting

We can use TS to interact with the DOM, just like with regular JS. For the most part, interacting in the DOM in TS is the same as with JS, but there are some key differences:

### Example 1

```
const anchor = document.querySelector('a');

console.log(anchor.href);
```

In TS, this would produce an error: `Object (anchor) is possibly null`. TS doesn't actually know whether there is an anchor tag during development. To take away this error in TS, we should first check that there actually is an anchor tag. 

```
if (anchor) console.log(anchor.href);
```

Alternatively, if we are certain that an anchor tag exists, we can add a `!` to the end of the query selector statement: `const anchor = document.querySelector('a')!`


### Special types for DOM elements

TS automatically contains special types for every DOM element. For example, the anchor that we selected would have the type `HTMLAnchorElement`. Thanks to these special types, we automatically have a bunch of associated methods on the element available. 


### Example 2

What if we are selecting a DOM element when there are several of that type of element on the same page? How can we bw certain that the selector statement will get us the right element? We could select it by the `class` of the specific element, which would work.

```
const form = document.querySelector('.form-one');
```

However, if we use the querySelector to select by something other than the html tag itself, the variable will be given a type of `Element`, rather than the specific type associated with the html element. A class can be applied to any element in html, so TS doesn't actually know what kind of element it is supposed to be. 

We can use **typecasting** to specify what type of element it is supposed to be:

```
const form = document.querySelector('form') as HTMLFormElement;
```
This way, it will be given the type associated with the form element, rather than the standard `Element` tag. 

Now let's try getting all of the input fields present inside the form. 

```
const invoiceType = document.querySelector('#invoiceType') as HTMLSelectElement;
const toFrom = document.querySelector('#toFrom') as HTMLInputElement;
const details = document.querySelector('#details') as HTMLInputElement;
const value = document.querySelector('#value') as HTMLInputElement;
```

Add an event listener to the form: 

```
form.addEventListener('submit', (e: Event) => {
  e.preventDefault();

  console.log(
    invoiceType.value,
    toFrom.value, 
    details.value, 
    details.valueAsNumber
  );
});
```

Note that for the value field, use the property `valueAsNumber` because by default, any numbers submitted into an HTML input (even with the number type of input) will be turned into a string on submission. 