---
> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*

---

# React.js Live-Task Mastery - Level 2 (Advanced)

This document covers advanced React patterns, system architecture, and optimization tasks commonly found in senior or lead-level interviews.

---

## **Section 1: Custom Hooks & Context (Q26-33)**

### **26. Build a custom useLocalStorage hook**
**Task:** Create a hook that syncs a state variable with the browser's localStorage.

#### **Solution:**
```jsx
import { useState, useEffect } from 'react';

function useLocalStorage(key, initialValue) {
  // Logic: Initialize from storage or use default
  const [value, setValue] = useState(() => {
    const saved = localStorage.getItem(key);
    return saved ? JSON.parse(saved) : initialValue;
  });

  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value)); // Update storage on change
  }, [key, value]);

  return [value, setValue];
}
```

---

### **27. Global Theme Context (Dark/Light)**
**Task:** Implement a Context provider that allows any child to access and toggle the current theme.

#### **Solution:**
```jsx
// Context.js
export const ThemeContext = React.createContext();

export const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState("light");
  const toggle = () => setTheme(prev => prev === "light" ? "dark" : "light");

  return (
    <ThemeContext.Provider value={{ theme, toggle }}>
      {children}
    </ThemeContext.Provider>
  );
};
```

---

### **28. Custom useFetch with Loading and Error**
**Task:** Create a hook that returns `{ data, loading, error }` for an API call.

#### **Solution:**
```jsx
function useFetch(url) {
  const [state, setState] = useState({ data: null, loading: true, error: null });

  useEffect(() => {
    setState({ data: null, loading: true, error: null }); // Reset on URL change
    fetch(url)
      .then(res => res.json())
      .then(data => setState({ data, loading: false, error: null }))
      .catch(err => setState({ data: null, loading: false, error: err.message }));
  }, [url]);

  return state;
}
```

---

### **29. Debounce an Input Value (Custom Hook)**
**Task:** Create a `useDebounce` hook to delay search updates until typing pauses for 500ms.

#### **Solution:**
```jsx
function useDebounce(value, delay) {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const handler = setTimeout(() => setDebouncedValue(value), delay);
    return () => clearTimeout(handler); // Cleanup: Cancel timeout if value changes fast
  }, [value, delay]);

  return debouncedValue;
}
```

---

### **30. Implement useReducer for a Shopping Cart**
**Task:** Handle complex state logic (Add, Remove, Clear) using `useReducer`.

#### **Solution:**
```jsx
const cartReducer = (state, action) => {
  switch (action.type) {
    case 'ADD': return [...state, action.payload];
    case 'REMOVE': return state.filter(it => it.id !== action.id);
    case 'CLEAR': return [];
    default: return state;
  }
};

function Cart() {
  const [items, dispatch] = useReducer(cartReducer, []);
  // Logic: dispatch({ type: 'ADD', payload: { id: 1, name: 'Book' } });
}
```

---

### **31. Persistent State between Route changes**
**Task:** Explain why a component loses state on navigation and how to prevent it.
**Scenario:** Moving from "Home" to "About" destroys the `Counter` state.

#### **Logic Board:**
| Method | Pro | Con |
|---|---|---|
| **Lifting to App.js** | Simple, no extra libs | Prop drilling if deep |
| **Context API** | Clean, widely accessible | Possible re-render issues |
| **Redux/Zustand** | Robust, structured | Boilerplate (Redux) |

---

### **32. Authentication Guardian (Higher-Order Component)**
**Task:** Create a `withAuth` HOC that redirects to `/login` if a user isn't authenticated.

#### **Solution:**
```jsx
const withAuth = (WrappedComponent) => {
  return (props) => {
    const { isAuthenticated } = useAuth(); // Assume custom hook
    if (!isAuthenticated) return <Redirect to="/login" />;
    return <WrappedComponent {...props} />;
  };
};
```

---

### **33. Manage Previous State with useRef**
**Task:** Track the *previous* value of a state variable and display it (e.g., "Count increased from 5 to 6").

#### **Solution:**
```jsx
function PrevTracker({ count }) {
  const prevCountRef = useRef();

  useEffect(() => {
    prevCountRef.current = count; // Updates AFTER render is finished
  });

  const prevCount = prevCountRef.current;
  return <h1>Now: {count}, Before: {prevCount}</h1>;
}
```

---

## **Section 2: Performance & Lifecycle (Q34-42)**

### **34. Memoize expensive results with useMemo**
**Task:** Filter a huge list of 10,000 items only when the search query changes.

#### **Solution:**
```jsx
const filteredTags = useMemo(() => {
  console.log("Expensive filter running...");
  return largeData.filter(item => item.includes(query));
}, [query, largeData]); // Re-calculates ONLY if these dependencies change
```

---

### **35. Prevent Parent-caused re-renders (React.memo)**
**Task:** Ensure a list item component ONLY re-renders when its specific data changes.

#### **Solution:**
```jsx
const ListRow = React.memo(({ item }) => {
  console.log("Rendering row:", item.id);
  return <li>{item.text}</li>;
}); // React.memo checks for shallow prop changes
```

---

### **36. Stabilization of Functions with useCallback**
**Task:** Pass a click handler to a memoized child without breaking its memoization.

#### **Solution:**
```jsx
function Parent() {
  const [count, setCount] = useState(0);

  // Logic: Without useCallback, this function is "new" on every Parent render
  const handleClick = useCallback(() => {
    console.log("Clicked!");
  }, []); // Stable identity

  return <MemoChild onClick={handleClick} />;
}
```

---

### **37. Handling Cleanup for race conditions (AbortController)**
**Task:** In a `useEffect` fetch, prevent data from an old request from overwriting new data.

#### **Solution:**
```jsx
useEffect(() => {
  const controller = new AbortController(); // Browser API

  fetch(url, { signal: controller.signal })
    .then(r => r.json())
    .then(data => setData(data))
    .catch(err => if (err.name !== 'AbortError') console.error(err));

  return () => controller.abort(); // Cancel request if URL changes or unmounts
}, [url]);
```

---

### **38. Focus Input on Mount (useRef)**
**Task:** Automatically focus the "Username" field when the Login modal opens.

#### **Solution:**
```jsx
function Modal() {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus(); // Access real DOM node via .current
  }, []);

  return <input ref={inputRef} placeholder="Enter name" />;
}
```

---

### **39. Sync State vs Layout (useLayoutEffect)**
**Task:** Measure a DOM element's width and set state *before* the browser paints it to avoid flickering.

#### **Solution:**
```jsx
useLayoutEffect(() => {
  const width = boxRef.current.offsetWidth;
  setBoxWidth(width); // Logic: Runs synchronously after DOM updates, before paint
}, []);
```

---

### **40. Error Boundary Implementation**
**Task:** Wrap a component so if it crashes, it shows a "Something went wrong" message instead of a white screen.

#### **Solution:**
```jsx
class ErrorBoundary extends React.Component {
  state = { hasError: false };

  static getDerivedStateFromError(error) {
    return { hasError: true }; // Updates state for UI fallback
  }

  render() {
    if (this.state.hasError) return <h1>Something went wrong.</h1>;
    return this.props.children;
  }
}
```

---

## **Section 4: System Design & Logic (Q41-50)**

### **41. Create a Modal with Portals**
**Task:** Render a modal outside the component's parent DOM hierarchy (e.g., at the body root).

#### **Solution:**
```jsx
import ReactDOM from 'react-dom';

const Modal = ({ isOpen, children }) => {
  if (!isOpen) return null;
  return ReactDOM.createPortal(
    <div className="modal">{children}</div>,
    document.getElementById('modal-root') // Destination in index.html
  );
};
```

---

### **42. Undo/Redo logic using State History**
**Task:** Implement "Undo" for a text input by keeping a history of previous strings.

#### **Solution:**
```jsx
function HistoryInput() {
  const [text, setText] = useState("");
  const [history, setHistory] = useState([]);

  const update = (newText) => {
    setHistory([...history, text]); // Save current to history
    setText(newText);
  };

  const undo = () => {
    const last = history[history.length - 1];
    setText(last);
    setHistory(history.slice(0, -1)); // Pop history
  };
}
```

---

### **43. Infinite Scroll Logic (Intersection Observer)**
**Task:** Trigger a `loadMore()` function when the bottom of a list is scrolled into view.

#### **Solution:**
```jsx
useEffect(() => {
  const observer = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) loadMore();
  });

  if (bottomRef.current) observer.observe(bottomRef.current);
  return () => observer.disconnect();
}, []);
```

---

### **44. Form Handling with useReducer**
**Task:** Manage a form with 10 fields using a single state object and a reducer.

#### **Solution:**
```jsx
const reducer = (state, action) => ({ ...state, [action.field]: action.value });

function Form() {
  const [formData, dispatch] = useReducer(reducer, { name: "", email: "" });
  const onChange = (e) => dispatch({ field: e.target.name, value: e.target.value });
}
```

---

### **45. Dynamic Component Injection**
**Task:** Render either `<CardLayout />` or `<ListLayout />` based on a variable.

#### **Solution:**
```jsx
const layouts = { card: CardLayout, list: ListLayout };

function View({ mode }) {
  const SelectedLayout = layouts[mode] || layouts.list;
  return <SelectedLayout data={data} />; // Dynamic component tag
}
```

---

### **46. Detecting Outside Clicks**
**Task:** Close a dropdown menu if the user clicks anywhere else on the page.

#### **Solution:**
```jsx
useEffect(() => {
  const checkOutside = (e) => {
    if (isOpen && ref.current && !ref.current.contains(e.target)) {
      setIsOpen(false); // Close menu
    }
  };
  document.addEventListener("mousedown", checkOutside);
  return () => document.removeEventListener("mousedown", checkOutside);
}, [isOpen]);
```

---

### **47. Sequential Effect Execution**
**Task:** Run Effect B only after Effect A has finished updating a specific state.

#### **Solution:**
```jsx
useEffect(() => {
  // Logic: Runs when 'initialized' becomes true
  if (initialized) console.log("System Ready!");
}, [initialized]); 
```

---

### **48. Managing Multiple API calls (Promise.all)**
**Task:** Fetch User data and Posts data simultaneously and show a spinner until both are ready.

#### **Solution:**
```jsx
useEffect(() => {
  Promise.all([fetch('/user').then(r=>r.json()), fetch('/posts').then(r=>r.json())])
    .then(([user, posts]) => {
       setData({ user, posts });
       setLoading(false);
    });
}, []);
```

---

### **49. Custom Hook: usePrevious**
**Task:** Encapsulate the "Previous value" logic into a reusable hook.

#### **Solution:**
```jsx
function usePrevious(value) {
  const ref = useRef();
  useEffect(() => {
    ref.current = value;
  });
  return ref.current; // Returns the value FROM THE PREVIOUS RENDER
}
```

---

### **50. Use EXPLAIN (React Profiler)**
**Task:** Identify which component is causing jank during a list scroll.

#### **Logic:**
1. Open Chrome DevTools -> **Profiler** tab.
2. Record the interaction.
3. Look for "Flamechart" spikes.
4. Check "Why did this render?" (requires DevTools setting enable).


---

> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*
> 
> *Share this resource on LinkedIn!*

---
