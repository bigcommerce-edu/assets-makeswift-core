# The Makeswift Approach to Components

## Reference Forwarding

**Example:**

```typescript
import { Ref, forwardRef } from 'react'

export const BlogList = forwardRef(
  (
    ref: Ref<HTMLUListElement>
  ) => {
    return (
      <ul ref={ref}>
        {/* ... */}
      </ul>
    )
  }
)
```

**Passing a ref:**

```typescript
import { useRef } from 'react';

export default function MyComponent() {
  const blogListRef = useRef(null);

  const someInteractiveFunction = () => {
    // Use blogListRef to access a DOM element
  }

  return (
    <BlogList ref={inputRef} />
  )
}
```

## Props and Controls

**Example:**

```typescript
type Props = {
  className?: string
  blogItems: {
    title: string
    author: string
    likeCount: number
  }[]
}

export const BlogList = forwardRef(
  (
    { className, blogItems }: Props,
    ref: Ref<HTMLUListElement>
  ) => {
    return (
      <ul className={clsx(className, 'w-full')} ref={ref}>
        {blogItems.map(item => (
          <BlogItem item={item} />
        )}
      </ul>
    )
  }
)
```

[Next](./02_ComponentControls.md)
