# react.js-cheat-sheet


# Guides
- https://www.w3schools.com/react/react_components.asp

# Extensions
- https://chromewebstore.google.com/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en&pli=1











<br><br>
<br><br>
________________________________
________________________________

<br><br>
<br><br>


# Templates

## List
- https://github.com/brillout/awesome-react-components


## UI Library

### nextui **hot**
- https://nextui.org

### tailwindui
- https://tailwindui.com/components

## MUI **hot**
- https://mui.com/material-ui/getting-started/usage/

### ant 
- https://ant.design/components/overview/

### chakra ui
- https://v2.chakra-ui.com/docs/components/container








<br><br>
<br><br>
________________________________
________________________________

<br><br>
<br><br>




# Components
- Use always unique name for a Component function

<br><br>

## RSC (React Server Components)
- Introduced in version 18 and it splitting components in two types

<br><br>

### Server components
- In next.js all components are server components by default
- They have the ability to run tasks like reading file or fetching data froma  database
- They can not handle user interactions

<br><br>

### Client components
- To create a client component you must add "use client" at the top of the component file
- Client components can not perform tasks like reading files  but they can use hooks and mange interactions


<br><br>
<br><br>


## Components in Components
```javascript
function Car() {
  return <h2>I am a Car!</h2>;
}

function Garage() {
  return (
    <>
      <h1>Who lives in my Garage?</h1>
      <Car />
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Garage />);
```
