
# React Context API

## What is Context API?
The **React Context API** is a built-in feature that allows you to share state across multiple components without the need for prop drilling. It provides a way to pass data through the component tree without manually passing props at every level.

### When to Use Context API?
- When you need to share state between multiple components.
- When you want to avoid **prop drilling**.
- When managing global state, such as:
  - **Theme switching** (Light/Dark mode)
  - **User authentication** (Logged-in state)
  - **Language settings**
  - **Cart state in an e-commerce app**

---

## Use Case: Theme Switching
A common use case for the Context API is managing **Light/Dark Mode** in an application.

### 1. Create `ThemeContext.js`
```jsx
import { createContext, useState } from "react";

// Create Theme Context
export const ThemeContext = createContext();

export const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState("light");

  // Toggle Theme
  const toggleTheme = () => {
    setTheme(theme === "light" ? "dark" : "light");
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
};
```

### 2. Wrap Your App with `ThemeProvider`
Modify `index.js` to include the provider:
```jsx
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";
import { ThemeProvider } from "./ThemeContext";

ReactDOM.render(
  <ThemeProvider>
    <App />
  </ThemeProvider>,
  document.getElementById("root")
);
```

### 3. Use the Context in `App.js`
```jsx
import { useContext } from "react";
import { ThemeContext } from "./ThemeContext";

const App = () => {
  const { theme, toggleTheme } = useContext(ThemeContext);

  return (
    <div style={{
      background: theme === "light" ? "#fff" : "#333",
      color: theme === "light" ? "#000" : "#fff",
      height: "100vh",
      display: "flex",
      alignItems: "center",
      justifyContent: "center",
      flexDirection: "column",
    }}>
      <h1>{theme === "light" ? "Light Mode" : "Dark Mode"}</h1>
      <button onClick={toggleTheme}>
        Switch to {theme === "light" ? "Dark" : "Light"} Mode
      </button>
    </div>
  );
};

export default App;
```

### Expected Behavior
- The application starts in **Light Mode**.
- Clicking the button toggles between **Light Mode** and **Dark Mode**.
- The theme state is managed globally using Context API, avoiding prop drilling.

---

## Conclusion
The **React Context API** simplifies state management for global data like themes, authentication, and language settings. It removes the need for complex state management libraries in simple use cases.

🚀 Happy Coding!

