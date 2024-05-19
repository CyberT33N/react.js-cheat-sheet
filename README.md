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












<br><br>
<br><br>
________________________________
________________________________

<br><br>
<br><br>


# Client components

<br><br>

## Data Fetching
- Because of CORS you can only make request to the same domain

<br><br>

### SWR
- **Not recommended when your data is changing each request**
- [https://swr.vercel.app/docs/arguments](https://swr.vercel.app/)
```javascript
import React from 'react'
import useSWR from 'swr'

const Fetch = async url => {
  const response = await fetch(url)

  if (!response.ok) {
    throw new Error('Failed to fetch data')
  }

  return await response.json()
}

export function NewCoinsGrid() {
  const { data, error } = useSWR('your-api-endpoint-key', Fetch);

  // Handle loading state and errors here (optional)
  if (error) return <div>Error fetching data: {error.message}</div>;
  if (!data) return <div>Loading...</div>;

   return (
     //... Your final render..
    )
}
```


### useEffect()
- We use useState() to define an empty array for the first init
  - setColumns() is the function which will be used after the request to our API is down to define the value of columns
    - headerColumns will work with columns and the get rendered successfully when setColumns(columns) was called
```javascript
import { useState, useRef, useEffect } from 'react'
import axios from 'axios'

export function NewCoinsGrid() {
    const [columns, setColumns] = useState([])
    const [error, setError] = useState(null)
    const [isLoading, setIsLoading] = useState(true)

    useEffect(() => {
        const fetchCoins = async() => {
            try {
                const res = await axios.get('/api/coins/discover/new')
                const { columns } = res.data
                setColumns(columns)
                setIsLoading(false)
            } catch (e) {
                setError(e.message)
            }
        }

        fetchCoins()
    }, [])

    const headerColumns = React.useMemo(() => {
        if (visibleColumns === 'all') return columns
        return columns.filter((column: any) => Array.from(visibleColumns).includes(column.uid))
    }, [visibleColumns, columns])

    if (isLoading) {
        return <div>Loading...</div> // Zeigen Sie eine Loading-Nachricht an, während die Daten geladen werden
    }

    if (error) {
        return <div>Error: {error}</div>
    }

    return (
     //... Your final render..
    )
}
```
