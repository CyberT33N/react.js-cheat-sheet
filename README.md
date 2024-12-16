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

<br><br>

## List
- https://github.com/brillout/awesome-react-components




<br><br>
<br><br>

## UI Library

### shadcn
- https://ui.shadcn.com/docs/installation/vite

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




# main.tsx

<details><summary>Click to expand..</summary>
  
- Ja, das ist tatsächlich der Standard-Ansatz in modernen React-Anwendungen, besonders wenn sie mit Build-Tools wie Vite oder Create React App erstellt wurden. Lass uns die wichtigsten Punkte durchgehen:

Standard-Struktur:
- Eine index.html mit einem Root-Element (<div id="root"></div>)
- Eine Haupt-TypeScript/JavaScript-Datei (traditionell index.tsx/index.js oder main.tsx/main.js), die als Einstiegspunkt dient
- Der Import dieser Datei in der index.html
  
Warum dieser Ansatz?:
- Saubere Trennung zwischen HTML-Grundgerüst und React-Anwendung
- Ermöglicht Client-Side-Rendering (CSR)
- Erlaubt das Bundling und Optimieren des JavaScript-Codes
- Ist kompatibel mit modernen Build-Tools und Hot Module Replacement (HMR)
  
Unterschiede in Namenskonventionen:
- Create React App verwendet traditionell index.js/index.tsx
- Vite (wie in deinem Projekt) verwendet standardmäßig main.js/main.tsx
- Die Funktionalität ist aber die gleiche
  
Der einzige Unterschied in deinem Setup zu anderen React-Projekten ist der Dateiname (main.tsx statt index.tsx), aber das ist nur eine Namenskonvention und ändert nichts an der Funktionsweise.
Diese Struktur ist bewährt und wird von der React-Community weitgehend als Best Practice angesehen.

index.html
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Kanban-Board</title>
    <meta name="description" content="This is a example of kanban board" />
    <meta name="author" content="CyberT33N" />
  </head>

  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
  </body>
</html>
```

main.tsx
```typescript
import { createRoot } from 'react-dom/client'
import App from './App.tsx'
import './index.css'

createRoot(document.getElementById("root")!).render(<App />);
```


</details>









<br><br>
<br><br>
________________________________
________________________________

<br><br>
<br><br>




# App.tsx
```typescript
// Theme und UI Komponenten Imports
import { ThemeProvider } from "@/components/theme-provider"
import { Toaster as Sonner } from "@/components/ui/sonner";
import { TooltipProvider } from "@/components/ui/tooltip";

// React Query für Datenmanagement
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";

// Routing Komponenten
import { BrowserRouter, Routes, Route } from "react-router-dom";

// Seiten Import
import Index from "./pages/Index";

// Erstelle eine neue Query Client Instanz für React Query
const queryClient = new QueryClient();

// Haupt App Komponente
const App = () => (
  // Theme Provider: Verwaltet das Farbschema der App (hell/dunkel)
  <ThemeProvider defaultTheme="dark" storageKey="vite-ui-theme">
    {/* Query Client Provider: Ermöglicht Datenabrufe und Caching in der gesamten App */}
    <QueryClientProvider client={queryClient}>
      {/* Tooltip Provider: Stellt Tooltip-Funktionalität bereit */}
      <TooltipProvider>
        {/* Toast Benachrichtigungskomponente für Feedback */}
        <Sonner />
        {/* Router Setup für Seitennavigation */}
        <BrowserRouter>
          <Routes>
            {/* Definiere die Hauptroute "/" */}
            <Route path="/" element={<Index />} />
          </Routes>
        </BrowserRouter>
      </TooltipProvider>
    </QueryClientProvider>
  </ThemeProvider>
);

export default App;
```




# React Router Komponenten Erklärung

<details><summary>Click to expand..</summary>

# Hauptkomponenten

## 1. BrowserRouter
- Basis-Router-Komponente für Web-Anwendungen
- Verwendet HTML5 History API für die URL-Manipulation
- Ermöglicht clientseitiges Routing ohne Seiten-Neuladen
- Muss die gesamte Routing-Logik umschließen

## 2. Routes
- Container für alle Route-Definitionen
- Vergleicht alle Kind-Routes gleichzeitig
- Wählt die beste übereinstimmende Route aus
- Rendert nur die passende Route-Komponente

## 3. Route
- Definiert eine einzelne Route in der Anwendung
- Wichtige Props:
  - `path`: URL-Pfad (z.B. "/about")
  - `element`: Komponente die gerendert wird

# Beispielverwendung
```tsx
<BrowserRouter>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/about" element={<About />} />
    <Route path="/users/:id" element={<UserProfile />} />
  </Routes>
</BrowserRouter>
```

</details>










<br><br>
<br><br>

## QueryClientProvider in React Query

<details><summary>Click to expand..</summary>
  

# Überblick
Der `QueryClientProvider` ist ein essentieller Bestandteil von React Query (TanStack Query), einer Bibliothek für effizientes Datenmanagement in React-Anwendungen.

# Hauptfunktionen

## 1. Caching
- Speichert Serverantworten zwischen
- Vermeidet unnötige API-Aufrufe
- Verbessert die Anwendungsperformance

## 2. Automatische Aktualisierung
- Hält Daten automatisch synchron
- Managed Background-Updates
- Stellt Datenaktualität sicher

## 3. Statusverwaltung
- Verwaltet Ladezustände
- Handhabt Fehlerzustände
- Bietet einfachen Zugriff auf Datenstatus

## 4. Optimistische Updates
- Ermöglicht UI-Updates vor Server-Antworten
- Verbessert gefühlte Performanz
- Bietet Fallback bei Fehlern

# Implementation in der App

```typescript
const queryClient = new QueryClient();

<QueryClientProvider client={queryClient}>
  {/* Kind-Komponenten haben Zugriff auf React Query */}
</QueryClientProvider>
```

Verwendungsbeispiel:
```typescript
// In einer Kind-Komponente:
const { data, isLoading } = useQuery({
  queryKey: ['todos'],
  queryFn: () => fetch('/api/todos').then(res => res.json())
});
```

</details>


Hauptvorteile
- Vereinfachtes API-Handling
- Automatisches Caching
- Retry-Mechanismen
- Lade- und Fehlerstatusmanagement
- Parallele und abhängige Abfragen
- Optimistische UI-Updates
- Der QueryClientProvider macht all diese Funktionen in der gesamten Anwendung verfügbar, indem er in der App.tsx eingebunden wird.













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




# Data Fetching
- Because of CORS you can only make request to the same domain

<br><br>

## SWR
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

<br><br>
<br><br>

## useEffect()
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

<br><br>
<br><br>

### Create interval
```
export async function GET() {
    const [data, setData] = useState(null);

    useEffect(() => {
        const fetchData = async () => {
            const result = await Fetch();
            setData(result);
        };

        fetchData(); // initialer Aufruf

        const interval = setInterval(() => {
            fetchData(); // Aufruf alle 5 Sekunden
        }, 5000);

        return () => clearInterval(interval); // Aufräumen beim unmounten
    }, []);

    if (!data) {
        return null; // Ladezustand handhaben
    }

    return Response.json(data);
}
```




























<br><br>
<br><br>
________________________________
________________________________

<br><br>
<br><br>



# Hooks


<br><br>
<br><br>


## useCallback
- useCallback is a React Hook that lets you cache a function definition between re-renders.
- https://react.dev/reference/react/useCallback
```typescript
import { useCallback } from 'react';

export default function ProductPage({ productId, referrer, theme }) {
  const handleSubmit = useCallback((orderDetails) => {
    post('/product/' + productId + '/buy', {
      referrer,
      orderDetails,
    });
  }, [productId, referrer]);
```
- If you want to setState inside then pass the variable to the array callback




<br><br>

## useMemo
- https://react.dev/reference/react/useMemo
- useMemo is a React Hook that lets you cache the result of a calculation between re-renders.

<br><br>

### Update Value
- Make sure that the data that has to been updated is to the second arg array
```typescript
const [lastUpdated, setLastUpdated] = useState(Date.now())


useEffect(() => {
    const interval = setInterval(() => {
        setLastUpdated(Date.now())
    }, 1000)

    return () => clearInterval(interval)
}, [])


const bottomContent = React.useMemo(() => {
    return (
            <div className="hidden sm:flex w-[30%] justify-end gap-2">
                <p>Last updated: {
                    Math.floor((Date.now() - lastUpdated) / 1000)} seconds ago ({
                    new Date().toLocaleTimeString()
                })</p>
            </div>
        </div>
    )
}, [lastUpdated)
```



























<br><br>
<br><br>
________________________________
________________________________

<br><br>
<br><br>

# Third Party Components

<br><br>

## Component Libary
- https://www.radix-ui.com/







## Toaster

### Sonner
- https://sonner.emilkowal.ski/

<details><summary>Click to expand..</summary>

@/components/ui/sonner
```typescript
import { useTheme } from "next-themes"
import { Toaster as Sonner } from "sonner"

type ToasterProps = React.ComponentProps<typeof Sonner>

const Toaster = ({ ...props }: ToasterProps) => {
  const { theme = "system" } = useTheme()

  return (
    <Sonner
      theme={theme as ToasterProps["theme"]}
      className="toaster group"
      toastOptions={{
        classNames: {
          toast:
            "group toast group-[.toaster]:bg-background group-[.toaster]:text-foreground group-[.toaster]:border-border group-[.toaster]:shadow-lg",
          description: "group-[.toast]:text-muted-foreground",
          actionButton:
            "group-[.toast]:bg-primary group-[.toast]:text-primary-foreground",
          cancelButton:
            "group-[.toast]:bg-muted group-[.toast]:text-muted-foreground",
        },
      }}
      {...props}
    />
  )
}

export { Toaster }
```

App.tsx
```
// Theme und UI Komponenten Imports
import { ThemeProvider } from "@/components/theme-provider"
import { Toaster } from "@/components/ui/toaster";
import { Toaster as Sonner } from "@/components/ui/sonner";
import { TooltipProvider } from "@/components/ui/tooltip";

// React Query für Datenmanagement
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";

// Routing Komponenten
import { BrowserRouter, Routes, Route } from "react-router-dom";

// Seiten Import
import Index from "./pages/Index";

// Erstelle eine neue Query Client Instanz für React Query
const queryClient = new QueryClient();

// Haupt App Komponente
const App = () => (
  // Theme Provider: Verwaltet das Farbschema der App (hell/dunkel)
  <ThemeProvider defaultTheme="dark" storageKey="vite-ui-theme">
    {/* Query Client Provider: Ermöglicht Datenabrufe und Caching in der gesamten App */}
    <QueryClientProvider client={queryClient}>
      {/* Tooltip Provider: Stellt Tooltip-Funktionalität bereit */}
      <TooltipProvider>
        {/* Toast Benachrichtigungskomponenten für Feedback */}
        <Toaster />
        <Sonner />
        {/* Router Setup für Seitennavigation */}
        <BrowserRouter>
          <Routes>
            {/* Definiere die Hauptroute "/" */}
            <Route path="/" element={<Index />} />
          </Routes>
        </BrowserRouter>
      </TooltipProvider>
    </QueryClientProvider>
  </ThemeProvider>
);

export default App;
```

</details>


  

<br><br>
<br><br>



## Tooltips

### Radix UI - Tooltip
- https://www.radix-ui.com/primitives/docs/components/tooltip

<details><summary>Click to expand..</summary>

@/components/ui/tooltip
```typescript
import * as React from "react"
import * as TooltipPrimitive from "@radix-ui/react-tooltip"

import { cn } from "@/lib/utils"

const TooltipProvider = TooltipPrimitive.Provider

const Tooltip = TooltipPrimitive.Root

const TooltipTrigger = TooltipPrimitive.Trigger

const TooltipContent = React.forwardRef<
  React.ElementRef<typeof TooltipPrimitive.Content>,
  React.ComponentPropsWithoutRef<typeof TooltipPrimitive.Content>
>(({ className, sideOffset = 4, ...props }, ref) => (
  <TooltipPrimitive.Content
    ref={ref}
    sideOffset={sideOffset}
    className={cn(
      "z-50 overflow-hidden rounded-md border bg-popover px-3 py-1.5 text-sm text-popover-foreground shadow-md animate-in fade-in-0 zoom-in-95 data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=closed]:zoom-out-95 data-[side=bottom]:slide-in-from-top-2 data-[side=left]:slide-in-from-right-2 data-[side=right]:slide-in-from-left-2 data-[side=top]:slide-in-from-bottom-2",
      className
    )}
    {...props}
  />
))
TooltipContent.displayName = TooltipPrimitive.Content.displayName

export { Tooltip, TooltipTrigger, TooltipContent, TooltipProvider }
```


App.tsx
```typescript
import { ThemeProvider } from "@/components/theme-provider"
import { Toaster } from "@/components/ui/toaster";
import { Toaster as Sonner } from "@/components/ui/sonner";
import { TooltipProvider } from "@/components/ui/tooltip";
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Index from "./pages/Index";

const queryClient = new QueryClient();

const App = () => (
  <ThemeProvider defaultTheme="dark" storageKey="vite-ui-theme">
    <QueryClientProvider client={queryClient}>
      <TooltipProvider>
        <Toaster />
        <Sonner />
        <BrowserRouter>
          <Routes>
            <Route path="/" element={<Index />} />
          </Routes>
        </BrowserRouter>
      </TooltipProvider>
    </QueryClientProvider>
  </ThemeProvider>
);

export default App;
```

</details>
