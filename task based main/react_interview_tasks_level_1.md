---
> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*

---

# React.js Live-Task Essentials - Level 1 (Fundamentals)

This guide provides 25 core React tasks designed for live coding assessments. Every solution includes literal code comments and logic boards to explain state transitions.

---

## **Section 1: Basic State & Hooks (Q1-10)**

### **1. Create a Simple Counter**
**Task:** Build a component that shows a number and has "Increment" and "Decrement" buttons.

#### **Solution:**
```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // Initialize state at 0

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Plus</button>   {/* Updates count +1 */}
      <button onClick={() => setCount(count - 1)}>Minus</button>  {/* Updates count -1 */}
    </div>
  );
}
```

#### **State Flow Board:**
| Action | Previous State | Logic | New State |
|---|---|---|---|
| Click Plus | 0 | 0 + 1 | 1 |
| Click Minus | 5 | 5 - 1 | 4 |

---

### **2. Toggle Visibility (Show/Hide)**
**Task:** Create a button that toggles the visibility of a "Secret Message" paragraph.

#### **Solution:**
```jsx
function ToggleMessage() {
  const [isVisible, setIsVisible] = useState(false); // Default: hidden

  return (
    <div>
      <button onClick={() => setIsVisible(!isVisible)}>
        {isVisible ? 'Hide' : 'Show'} Secret
      </button>
      {isVisible && <p>I am a secret!</p>} {/* Logic: If true, show P */}
    </div>
  );
}
```

---

### **3. Controlled Input (Mirror Text)**
**Task:** Create an input field where the text typed is instantly mirrored underneath it.

#### **Solution:**
```jsx
function MirrorInput() {
  const [text, setText] = useState('');

  return (
    <div>
      <input 
        type="text" 
        value={text}                 // Bind value to state
        onChange={(e) => setText(e.target.value)} // Sync state on change
      />
      <p>Typing: {text}</p>
    </div>
  );
}
```

---

### **4. Render a List from an Array**
**Task:** Given an array `const names = ["Alice", "Bob", "Charlie"]`, render them as an `<ul>`.

#### **Solution:**
```jsx
function NameList() {
  const names = ["Alice", "Bob", "Charlie"];

  return (
    <ul>
      {names.map((name, index) => (
        <li key={index}>{name}</li> // key is required for React reconciliation
      ))}
    </ul>
  );
}
```

---

### **5. Pass Data via Props (Parent to Child)**
**Task:** Create a `UserCard` child component that receives `name` and `role` from a parent `App` component.

#### **Solution:**
```jsx
// Child
const UserCard = (props) => (
  <div className="card">
    <h3>{props.name}</h3>     {/* Access data via props object */}
    <p>Role: {props.role}</p>
  </div>
);

// Parent
function App() {
  return <UserCard name="Rahul" role="Developer" />; // Send data as attributes
}
```

---

### **6. Fetch Data on Mount (useEffect)**
**Task:** Fetch a list of users from `https://api.example.com/users` when the component first loads.

#### **Solution:**
```jsx
import { useEffect, useState } from 'react';

function UserLoader() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch('https://api.example.com/users')
      .then(res => res.json())
      .then(data => setUsers(data)); // Set state with API result
  }, []); // Empty array means: "Only run on first mount"

  return <div>Loaded {users.length} users</div>;
}
```

#### **Execution Flow Board:**
| Phase | Action | Result |
|---|---|---|
| Render 1 | Initialization | `users` is `[]` |
| **Effect** | `fetch()` called | Network request starts |
| Render 2 | `setUsers()` called | UI updates with data |

---

### **7. Cleanup in useEffect (Window Resize)**
**Task:** Track the window width and update it in real-time, ensuring listeners are cleaned up.

#### **Solution:**
```jsx
function WindowTracker() {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    const handleResize = () => setWidth(window.innerWidth);
    window.addEventListener('resize', handleResize);

    return () => {
      // Logic: This runs when component unmounts
      window.removeEventListener('resize', handleResize);
    };
  }, []);

  return <h1>Width: {width}px</h1>;
}
```

---

### **8. Simple Form Submission**
**Task:** Create a login form that alerts the username on submit and prevents page reload.

#### **Solution:**
```jsx
function LoginForm() {
  const [user, setUser] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault(); // Stop page refresh
    alert(`Welcome, ${user}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input onChange={(e) => setUser(e.target.value)} />
      <button type="submit">Login</button>
    </form>
  );
}
```

---

### **9. Character Counter**
**Task:** Create a textarea with a real-time character count. Change the color to red if it exceeds 50.

#### **Solution:**
```jsx
function CharCounter() {
  const [msg, setMsg] = useState("");
  const limit = 50;

  return (
    <div>
      <textarea onChange={(e) => setMsg(e.target.value)} />
      <p style={{ color: msg.length > limit ? 'red' : 'green' }}>
        Count: {msg.length} / {limit}
      </p>
    </div>
  );
}
```

---

### **10. Simple Search Filter**
**Task:** Filter a local array of items based on what the user types in an input.

#### **Solution:**
```jsx
function SearchList() {
  const items = ["Apple", "Banana", "Cherry", "Date"];
  const [query, setQuery] = useState("");

  const filtered = items.filter(item => 
    item.toLowerCase().includes(query.toLowerCase())
  );

  return (
    <div>
      <input onChange={(e) => setQuery(e.target.value)} placeholder="Search..." />
      {filtered.map(item => <p key={item}>{item}</p>)}
    </div>
  );
}
```

---

## **Section 2: Communication & Rendering (Q11-20)**

### **11. Lifting State Up**
**Task:** Parent manages a `count` state, but two separate sibling components (`Button` and `Display`) interact with it.

#### **Solution:**
```jsx
function Parent() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <Display value={count} />
      <Button onClick={() => setCount(count + 1)} />
    </div>
  );
}

const Display = ({ value }) => <h1>Value: {value}</h1>;
const Button = ({ onClick }) => <button onClick={onClick}>Add</button>;
```

---

### **12. Checkbox handling (Handle Multiple)**
**Task:** Track whether "Agree to terms" and "Subscribe to Newsletter" are checked.

#### **Solution:**
```jsx
function Settings() {
  const [prefs, setPrefs] = useState({ terms: false, news: false });

  const toggle = (field) => {
    setPrefs({ ...prefs, [field]: !prefs[field] }); // Spread & Toggle
  };

  return (
    <div>
      <input type="checkbox" onChange={() => toggle('terms')} /> Agree
      <input type="checkbox" onChange={() => toggle('news')} /> News
    </div>
  );
}
```

---

### **13. Render Children (props.children)**
**Task:** Create a `Container` component that adds a border and padding around whatever is placed inside it.

#### **Solution:**
```jsx
const Container = ({ children }) => (
  <div style={{ border: '2px solid blue', padding: '20px' }}>
    {children} {/* Renders nested content */}
  </div>
);

function App() {
  return (
    <Container>
      <h1>I am inside the box!</h1>
    </Container>
  );
}
```

---

### **14. Dynamic Styling (Class Toggle)**
**Task:** Clicking a div toggles its background color between "Light" and "Dark".

#### **Solution:**
```jsx
function ThemeToggle() {
  const [isDark, setIsDark] = useState(false);

  return (
    <div 
      className={isDark ? "bg-dark" : "bg-light"} // Dynamic class attribution
      onClick={() => setIsDark(!isDark)}
      style={{ width: '100px', height: '100px', cursor: 'pointer' }}
    >
      Click Me
    </div>
  );
}
```

---

### **15. Conditional logic (Ternary vs AND)**
**Task:** Show "Logout" button if `isLoggedIn` is true, otherwise show "Login". Also show "Admin" text ONLY if `isAdmin` is true.

#### **Solution:**
```jsx
function Nav({ isLoggedIn, isAdmin }) {
  return (
    <nav>
      {isLoggedIn ? <button>Logout</button> : <button>Login</button>}
      {isLoggedIn && isAdmin && <span>Welcome Admin</span>}
    </nav>
  );
}
```

---

### **16. Input validation on change**
**Task:** Show a "Password must be 8+ chars" error in red if the password length is too short.

#### **Solution:**
```jsx
function Signup() {
  const [pw, setPw] = useState("");

  return (
    <div>
      <input type="password" onChange={(e) => setPw(e.target.value)} />
      {pw.length > 0 && pw.length < 8 && (
        <small style={{ color: 'red' }}>Too short!</small>
      )}
    </div>
  );
}
```

---

### **17. Image Slider (Manual)**
**Task:** Click "Next" and "Prev" to cycle through an array of 3 image URLs.

#### **Solution:**
```jsx
function Slider() {
  const images = ["img1.jpg", "img2.jpg", "img3.jpg"];
  const [idx, setIdx] = useState(0);

  const next = () => setIdx((idx + 1) % images.length); // Loop back to 0
  const prev = () => setIdx((idx - 1 + images.length) % images.length);

  return (
    <div>
      <button onClick={prev}>Prev</button>
      <img src={images[idx]} alt="slide" />
      <button onClick={next}>Next</button>
    </div>
  );
}
```

---

### **18. Accordion (Single Active Item)**
**Task:** Create a list of 3 items. Clicking one expands it and closes the others.

#### **Solution:**
```jsx
function Accordion() {
  const [activeId, setActiveId] = useState(null); // Store ID of open item

  const items = [
    { id: 1, text: "Panel 1 content" },
    { id: 2, text: "Panel 2 content" }
  ];

  return (
    <div>
      {items.map(item => (
        <div key={item.id} onClick={() => setActiveId(item.id)}>
          <h3>Header {item.id}</h3>
          {activeId === item.id && <p>{item.text}</p>}
        </div>
      ))}
    </div>
  );
}
```

---

### **19. Countdown Timer (useEffect)**
**Task:** Create a timer that starts at 10 and stops at 0.

#### **Solution:**
```jsx
function Countdown() {
  const [val, setVal] = useState(10);

  useEffect(() => {
    if (val === 0) return; // Stop at zero

    const timer = setInterval(() => {
      setVal(v => v - 1); // Functional update to avoid stale state
    }, 1000);

    return () => clearInterval(timer); // Critical: stop on unmount
  }, [val]); // Dependency: restart logic when val changes

  return <h1>T-Minus: {val}</h1>;
}
```

---

### **20. Dropdown Selection**
**Task:** Pick a fruit from a `<select>` dropdown and display a custom message like "You picked Apple".

#### **Solution:**
```jsx
function FruitSelect() {
  const [fruit, setFruit] = useState("Apple");

  return (
    <div>
      <select value={fruit} onChange={(e) => setFruit(e.target.value)}>
        <option>Apple</option>
        <option>Orange</option>
      </select>
      <p>Choice: {fruit}</p>
    </div>
  );
}
```

---

## **Section 3: Arrays & Operations (Q21-25)**

### **21. Passing Functions as Props**
**Task:** Child component has a button that, when clicked, changes the parent's background color.

#### **Solution:**
```jsx
const ColorButton = ({ color, update }) => (
  <button onClick={() => update(color)}>Make {color}</button>
);

function App() {
  const [bg, setBg] = useState("white");

  return (
    <div style={{ background: bg }}>
      <ColorButton color="red" update={setBg} />
      <ColorButton color="blue" update={setBg} />
    </div>
  );
}
```

---

### **22. Responsive Navbar Toggle**
**Task:** Create a mobile menu that opens/closes when the "Hamburger" icon is clicked.

#### **Solution:**
```jsx
function Navbar() {
  const [isOpen, setIsOpen] = useState(false);

  return (
    <nav>
      <div className="hamburger" onClick={() => setIsOpen(!isOpen)}>☰</div>
      <ul className={isOpen ? "menu-open" : "menu-closed"}>
        <li>Home</li>
        <li>About</li>
      </ul>
    </nav>
  );
}
```

---

### **23. Todo List: Add Item**
**Task:** Add a string from an input field into an array state on button click.

#### **Solution:**
```jsx
function TodoAdd() {
  const [list, setList] = useState([]);
  const [val, setVal] = useState("");

  const add = () => {
    if (!val) return;
    setList([...list, val]); // Create new array with old items + new one
    setVal("");              // Clear input
  };

  return (
    <div>
      <input value={val} onChange={(e) => setVal(e.target.value)} />
      <button onClick={add}>Add</button>
      {list.map((it, i) => <li key={i}>{it}</li>)}
    </div>
  );
}
```

---

### **24. Todo List: Delete Item**
**Task:** Add a "Delete" button next to each Todo item that removes it from the list.

#### **Solution:**
```jsx
function TodoFull() {
  const [list, setList] = useState(["Eat", "Code", "Sleep"]);

  const remove = (idx) => {
    // Logic: Filter produces a new array excluding the target index
    const updated = list.filter((_, i) => i !== idx);
    setList(updated);
  };

  return (
    <ul>
      {list.map((it, i) => (
        <li key={i}>
          {it} <button onClick={() => remove(i)}>X</button>
        </li>
      ))}
    </ul>
  );
}
```

---

### **25. Map with Fallback (Empty State)**
**Task:** Render a list of items, but if the list is empty, show "No items found".

#### **Solution:**
```jsx
function SmartList({ items }) {
  // If array doesn't exist or is empty, show fallback
  if (!items || items.length === 0) {
    return <p>No items found.</p>;
  }

  return (
    <ul>
      {items.map(it => <li key={it.id}>{it.name}</li>)}
    </ul>
  );
}
```


---

> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*
> 
> *Share this resource on LinkedIn!*

---
