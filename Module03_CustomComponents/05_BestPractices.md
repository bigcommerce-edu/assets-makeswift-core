# Best Practices

## React Best Practices

### Using State Appropriately

**Incorrect use of state after change:**

```javascript
const [count, setCount] = useState(0)

const onClick = () => {
  setCount(count + 1)
  alert(count)
}
```

**Correct use of separate var for new value:**

```javascript
const [count, setCount] = useState(0)

const onClick = () => {
  const newCount = count + 1
  setCount(newCount)
  alert(newCount)
}
```

### Using State and Props Together

**Incorrect use of state with props:**

```javascript
const MyComponent = forwardRef((
  {
    lightColor,
    darkColor,
  },
  ref
) => {
  const [textColor, setTextColor] = useState(lightColor)

  const onModeChange = (mode) => {
    setTextColor(mode === "light" ? lightColor : darkColor)
  }

  // ... use textColor in JSX
})
```

**useEffect with props as dependencies:**

```javascript
const MyComponent = forwardRef((
  {
    lightColor,
    darkColor,
  },
  ref
) => {
  const [textColor, setTextColor] = useState(lightColor)

  useEffect(() => {
    setTextColor(mode === "light" ? lightColor : darkColor)
  }, [lightColor, darkColor])

  const onModeChange = (mode) => {
    setTextColor(mode === "light" ? lightColor : darkColor)
  }

  // ... use textColor in JSX
})
```

**Compute from props and state:**

```javascript
const MyComponent = forwardRef((
  {
    lightColor,
    darkColor,
  },
  ref
) => {
  const [mode, setMode] = useState("light")

  const onModeChange = (mode) => {
    setMode(mode)  
  }

  const textColor = (mode === "light") ? lightColor : darkColor

  // ... use textColor in JSX
})
```

[Next](../Module04_HandsOnLabs/01_ProjectSetup.md)
