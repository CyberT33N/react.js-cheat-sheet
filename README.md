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

<details><summary>Click to expand..</summary>

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


</details>





























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




Hauptvorteile
- Vereinfachtes API-Handling
- Automatisches Caching
- Retry-Mechanismen
- Lade- und Fehlerstatusmanagement
- Parallele und abhängige Abfragen
- Optimistische UI-Updates
- Der QueryClientProvider macht all diese Funktionen in der gesamten Anwendung verfügbar, indem er in der App.tsx eingebunden wird.

</details>







































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

<details><summary>Click to expand..</summary>

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

</details>


























<br><br>
<br><br>
________________________________
________________________________

<br><br>
<br><br>


# React Hooks

<details><summary>Click to expand..</summary>

  
## useState

- `useState` is a React Hook that lets you add state to functional components.
- It returns an array with two values: the current state and a function to update it.

### Example
```typescript
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

---

## useEffect

- `useEffect` is a React Hook that lets you perform side effects in your components.
- It runs after the render and optionally cleans up after the effect.

### Example
```typescript
import { useEffect } from 'react';

function App() {
  useEffect(() => {
    console.log('Component mounted');
    return () => console.log('Component unmounted');
  }, []); // Empty dependency array: runs only on mount and unmount
}
```

---

## useContext

- `useContext` lets you access values from React's Context API in your components.
- You can avoid passing props down manually through many levels.

### Example
```typescript
import { useContext } from 'react';
import { ThemeContext } from './ThemeContext';

function App() {
  const theme = useContext(ThemeContext);
  return <div style={{ background: theme.background }}>Hello!</div>;
}
```

---

## useReducer

- `useReducer` is a React Hook that lets you manage complex state logic.
- It is an alternative to `useState` when state transitions become complex.

### Example
```typescript
import { useReducer } from 'react';

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
      <span>{state.count}</span>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
    </>
  );
}
```

---

## useCallback

- `useCallback` caches a function between re-renders, preventing unnecessary re-creation.
- It is useful when passing callbacks to child components.

### Example
```typescript
import { useCallback } from 'react';

function App({ productId }) {
  const handleClick = useCallback(() => {
    console.log('Product ID:', productId);
  }, [productId]);

  return <button onClick={handleClick}>Log Product ID</button>;
}
```

---

## useMemo

- `useMemo` caches the result of a computation between renders.
- It is used to optimize performance by skipping expensive calculations.

### Example
```typescript
import { useMemo } from 'react';

function App({ items }) {
  const expensiveCalculation = useMemo(() => {
    return items.reduce((sum, item) => sum + item.value, 0);
  }, [items]);

  return <div>Total: {expensiveCalculation}</div>;
}
```

---

## useRef

- `useRef` provides a mutable reference to a DOM element or a value that persists across renders.

### Example
```typescript
import { useRef } from 'react';

function App() {
  const inputRef = useRef();

  const focusInput = () => {
    inputRef.current.focus();
  };

  return (
    <>
      <input ref={inputRef} />
      <button onClick={focusInput}>Focus Input</button>
    </>
  );
}
```

---

## useImperativeHandle

- `useImperativeHandle` customizes the instance value exposed when using `React.forwardRef`.

### Example
```typescript
import React, { useImperativeHandle, useRef, forwardRef } from 'react';

const CustomInput = forwardRef((props, ref) => {
  const inputRef = useRef();
  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    },
  }));
  return <input ref={inputRef} />;
});

function App() {
  const ref = useRef();

  return (
    <>
      <CustomInput ref={ref} />
      <button onClick={() => ref.current.focus()}>Focus Input</button>
    </>
  );
}
```

---

## useLayoutEffect

- `useLayoutEffect` runs synchronously after all DOM mutations but before the browser paints.
- Use it for DOM measurements or mutations.

### Example
```typescript
import { useLayoutEffect, useRef } from 'react';

function App() {
  const ref = useRef();

  useLayoutEffect(() => {
    console.log(ref.current.getBoundingClientRect());
  }, []);

  return <div ref={ref}>Hello</div>;
}
```

---

## useDebugValue

- `useDebugValue` lets you display custom labels for hooks in React DevTools.

### Example
```typescript
import { useDebugValue, useState } from 'react';

function useCustomHook() {
  const [value, setValue] = useState(0);
  useDebugValue(value > 5 ? 'High' : 'Low');
  return [value, setValue];
}
```

---

## useId

- `useId` generates unique IDs for accessibility and server rendering.

### Example
```typescript
import { useId } from 'react';

function App() {
  const id = useId();

  return <label htmlFor={id}>Name: <input id={id} /></label>;
}
```

---

## useTransition

- `useTransition` lets you mark updates as non-urgent and improve UI responsiveness.

### Example
```typescript
import { useState, useTransition } from 'react';

function App() {
  const [isPending, startTransition] = useTransition();
  const [count, setCount] = useState(0);

  const handleClick = () => {
    startTransition(() => {
      setCount((c) => c + 1);
    });
  };

  return (
    <div>
      <button onClick={handleClick}>Increment</button>
      {isPending ? 'Updating...' : count}
    </div>
  );
}
```

---

## useDeferredValue

- `useDeferredValue` lets you delay updating a non-urgent state.

### Example
```typescript
import { useState, useDeferredValue } from 'react';

function App() {
  const [value, setValue] = useState('');
  const deferredValue = useDeferredValue(value);

  return (
    <>
      <input onChange={(e) => setValue(e.target.value)} />
      <p>Deferred: {deferredValue}</p>
    </>
  );
}
```


</details>









































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







<br><br>

## Icon

<br><br>

## lucide-react
- https://lucide.dev/guide/packages/lucide-react











<br><br>
<br><br>

## Drag and Drop

<br><br>

### @hello-pangea/dnd
- https://github.com/hello-pangea/dnd

<details><summary>Click to expand..</summary>

```typescript
// Import von React und dem State-Management
import React, { useState } from 'react';
// Import der Drag & Drop Funktionalität
import { DragDropContext, Droppable } from '@hello-pangea/dnd';
// Import der Icons für die UI
import { Plus, MoreHorizontal, Pencil, Trash2 } from 'lucide-react';
// Import der UI Komponenten
import { Button } from '@/components/ui/button';
import { Input } from '@/components/ui/input';
import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuTrigger,
} from '@/components/ui/dropdown-menu';
import KanbanColumn from './KanbanColumn';
import { toast } from 'sonner';

// Definition des Case-Typs für einzelne Karten
/**
 * Ein Case repräsentiert eine einzelne Karte auf dem Kanban-Board.
 * Es hat eine eindeutige ID, einen Titel und ein Update-Datum.
 */
export type Case = {
  id: string;
  title: string;
  updatedAt: string;
};

// Definition des Column-Typs für Spalten
/**
 * Eine Column repräsentiert eine Spalte auf dem Kanban-Board.
 * Sie hat eine eindeutige ID, einen Titel und eine Liste von Cases.
 */
export type Column = {
  id: string;
  title: string;
  cases: Case[];
};

const KanbanBoard = () => {
  // State für die Kanban-Spalten mit Initial-Daten
  /**
   * Der State für die Kanban-Spalten wird initialisiert mit vier Spalten:
   * TODO, IN PROGRESS, DONE und ARCHIVED.
   */
  const [columns, setColumns] = useState<Column[]>([
    {
      id: 'todo',
      title: 'TODO',
      cases: [
        { id: '1', title: 'Case 1', updatedAt: '3 days ago' },
        { id: '2', title: 'Case 2', updatedAt: '3 days ago' },
      ],
    },
    {
      id: 'in-progress',
      title: 'IN PROGRESS',
      cases: [
        { id: '3', title: 'Case 3', updatedAt: '3 days ago' },
      ],
    },
    {
      id: 'done',
      title: 'DONE',
      cases: [
        { id: '4', title: 'Case 4', updatedAt: '3 days ago' },
      ],
    },
    {
      id: 'archived',
      title: 'ARCHIVED',
      cases: [],
    },
  ]);

  // State für die aktuell bearbeitete Spalte
  /**
   * Der State für die aktuell bearbeitete Spalte wird initialisiert mit null.
   * Wenn eine Spalte bearbeitet wird, wird ihre ID hier gespeichert.
   */
  const [editingColumn, setEditingColumn] = useState<string | null>(null);

  // Handler für das Ende einer Drag & Drop Operation
  /**
   * Wenn eine Drag & Drop Operation beendet wird, wird dieser Handler aufgerufen.
   * Er aktualisiert die Position der Cases in den Spalten entsprechend.
   */
  const handleDragEnd = (result: any) => {
    if (!result.destination) return;

    const { source, destination } = result;

    if (source.droppableId === destination.droppableId) {
      // Neuanordnung innerhalb derselben Spalte
      const column = columns.find(col => col.id === source.droppableId);
      if (!column) return;

      const newCases = Array.from(column.cases);
      const [removed] = newCases.splice(source.index, 1);
      newCases.splice(destination.index, 0, removed);

      setColumns(columns.map(col => 
        col.id === source.droppableId ? { ...col, cases: newCases } : col
      ));
    } else {
      // Verschieben zwischen verschiedenen Spalten
      const sourceColumn = columns.find(col => col.id === source.droppableId);
      const destColumn = columns.find(col => col.id === destination.droppableId);
      if (!sourceColumn || !destColumn) return;

      const sourceCases = Array.from(sourceColumn.cases);
      const destCases = Array.from(destColumn.cases);
      const [removed] = sourceCases.splice(source.index, 1);
      destCases.splice(destination.index, 0, removed);

      setColumns(columns.map(col => {
        if (col.id === source.droppableId) {
          return { ...col, cases: sourceCases };
        }
        if (col.id === destination.droppableId) {
          return { ...col, cases: destCases };
        }
        return col;
      }));

      toast.success(`Case moved to ${destColumn.title}`);
    }
  };

  // Funktion zum Hinzufügen eines neuen Cases
  /**
   * Diese Funktion fügt ein neues Case zu einer Spalte hinzu.
   * Das neue Case erhält eine eindeutige ID, einen Titel und ein Update-Datum.
   */
  const addNewCase = (columnId: string) => {
    const newCase: Case = {
      id: Math.random().toString(36).substr(2, 9),
      title: `Case ${Math.floor(Math.random() * 1000)}`,
      updatedAt: 'Just now',
    };

    setColumns(columns.map(col => 
      col.id === columnId 
        ? { ...col, cases: [newCase, ...col.cases] }
        : col
    ));

    toast.success('New case created');
  };

  // Funktion zum Hinzufügen einer neuen Spalte
  /**
   * Diese Funktion fügt eine neue Spalte zum Kanban-Board hinzu.
   * Die neue Spalte erhält eine eindeutige ID, einen Titel und eine leere Liste von Cases.
   */
  const addNewColumn = () => {
    const newColumn: Column = {
      id: Math.random().toString(36).substr(2, 9),
      title: 'New Column',
      cases: [],
    };

    setColumns([...columns, newColumn]);
    setEditingColumn(newColumn.id);
    toast.success('New column added');
  };

  // Funktion zum Löschen einer Spalte
  /**
   * Diese Funktion löscht eine Spalte vom Kanban-Board.
   * Alle Cases in der Spalte werden gelöscht.
   */
  const deleteColumn = (columnId: string) => {
    setColumns(columns.filter(col => col.id !== columnId));
    toast.success('Column deleted');
  };

  // Funktion zum Aktualisieren des Spaltentitels
  /**
   * Diese Funktion aktualisiert den Titel einer Spalte.
   * Der neue Titel wird im State gespeichert.
   */
  const updateColumnTitle = (columnId: string, newTitle: string) => {
    setColumns(columns.map(col => 
      col.id === columnId ? { ...col, title: newTitle } : col
    ));
    setEditingColumn(null);
  };

  return (
    <div className="p-6">
      {/* Header mit Titel und "Add Column" Button */}
      <div className="flex justify-between items-center mb-6">
        <h1 className="text-2xl font-bold">Board</h1>
        <Button onClick={addNewColumn} variant="outline" size="sm">
          <Plus className="w-4 h-4 mr-2" />
          Add Column
        </Button>
      </div>
      
      {/* Drag & Drop Kontext für das gesamte Board */}
      <DragDropContext onDragEnd={handleDragEnd}>
        <div className="flex gap-6 overflow-x-auto pb-4">
          {columns.map((column, index) => (
            <div key={column.id} className="kanban-column">
              {/* Spalten-Header mit Titel und Optionen */}
              <div className="kanban-header mb-4">
                {editingColumn === column.id ? (
                  <Input
                    autoFocus
                    defaultValue={column.title}
                    onBlur={(e) => updateColumnTitle(column.id, e.target.value)}
                    onKeyDown={(e) => {
                      if (e.key === 'Enter') {
                        updateColumnTitle(column.id, e.currentTarget.value);
                      }
                    }}
                  />
                ) : (
                  <div className="flex items-center justify-between w-full">
                    <span>{column.title}</span>
                    {/* Dropdown-Menü für Spaltenaktionen */}
                    <DropdownMenu>
                      <DropdownMenuTrigger asChild>
                        <Button variant="ghost" size="sm">
                          <MoreHorizontal className="w-4 h-4" />
                        </Button>
                      </DropdownMenuTrigger>
                      <DropdownMenuContent>
                        <DropdownMenuItem onClick={() => setEditingColumn(column.id)}>
                          <Pencil className="w-4 h-4 mr-2" />
                          Rename
                        </DropdownMenuItem>
                        <DropdownMenuItem 
                          className="text-destructive"
                          onClick={() => deleteColumn(column.id)}
                        >
                          <Trash2 className="w-4 h-4 mr-2" />
                          Delete
                        </DropdownMenuItem>
                      </DropdownMenuContent>
                    </DropdownMenu>
                  </div>
                )}
              </div>

              {/* Droppable Bereich für Cases */}
              <Droppable droppableId={column.id}>
                {(provided) => (
                  <div
                    ref={provided.innerRef}
                    {...provided.droppableProps}
                    className="min-h-[200px]"
                  >
                    <KanbanColumn cases={column.cases} />
                    {provided.placeholder}
                  </div>
                )}
              </Droppable>

              {/* "Create Case" Button nur in der ersten Spalte */}
              {index === 0 && (
                <Button 
                  onClick={() => addNewCase(column.id)}
                  variant="ghost" 
                  className="w-full mt-4"
                >
                  <Plus className="w-4 h-4 mr-2" />
                  Create Case
                </Button>
              )}
            </div>
          ))}
        </div>
      </DragDropContext>
    </div>
  );
};

export default KanbanBoard;
```

</details>






















<br><br>
<br><br>




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
