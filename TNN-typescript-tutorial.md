# TypeScript tutorial (The Net Ninja)

[link to playlist](https://www.youtube.com/watch?v=2pZmKW9-I_k&list=PL4cUxeGkcC9gUgr39Q_yD6v-bSyMwKPUI)

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

If we chack the compiled code in the JS file, we can see that it has changed `const` into `var`. The console log also now shows up in the browser. 

However, there is now an error popping up in the TS file: `cannot re-declare block-scoped variable 'character'`. This is just happening if both the TS and JS files are open at the same time. If we close one file, the error will go away. 

For now, every time we change the TS file, we need to manually recomiple it to the JS file. We would rather watch for the file constantly and only run the command once- to do this we can run: 

`tsc sandbox.ts -w` which watches for changes in the file and compiles automatically. 


