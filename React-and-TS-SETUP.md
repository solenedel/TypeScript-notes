# How to set up TypeScript with a React app

[tutorial link](https://www.youtube.com/watch?v=I9jfsIRnySs)

## 1A - If the project is not created yet

There is a special command so tell create-react-app to use typescript from the beginning. [link](https://create-react-app.dev/docs/adding-typescript/)

`npx create-react-app my-app --template typescript`

## 1B - If the project already exists

If  `create-react-app` has already been run without specifying TS, run this command:

`npm install --save typescript @types/node @types/react @types/react-dom @types/jest`

Next, rename any file to be a TypeScript file (e.g. src/index.js to src/index.tsx) and restart your development server.

## Generate tsconfig file

If the tsconfig file does not exist yet, generate it with `tsx --init`