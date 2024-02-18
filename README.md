# react.js-cheat-sheet





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
