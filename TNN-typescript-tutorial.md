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




