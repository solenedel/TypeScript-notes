# Using TypeScript in a React app

[link](https://www.youtube.com/watch?v=z8lDwLKthr8)


## General rules

- In every file that contains JSX (a `.jsx` file), you must use the `.tsx` extension instead.
- Files that are `.js` for example helper helper functions should be changed to `.ts`

## Props

Example: passing a title prop to the Heading component:

```
function Heading( { title }: { title: string }) {
  return <h1>{title}</h1>
}

function App() {
  return (
    <div>
    <Heading title="hello there" />
    </div>
  )
}
```
