# Component Controls

## Introduction

**Registration example:**

```typescript
import { TextInput } from '@makeswift/runtime/controls'

runtime.registerComponent(
  lazy(() => import('./MyComponent')),
  {
    type: 'my-component',
    label: 'My Component',
    props: {
      title: TextInput({
        label: "Title",
        defaultValue: "Example Title",
      }),
    },
  }
)
```

**Receiving props example:**

```typescript
export const MyComponent = forwardRef(
  (
    { title }: { title: string },
    ref: Ref<HTMLDivElement>
  ) => {
    return (
      <div ref={ref}>
        <h1>{title}</h1>
      </div>
    )
  }
)
```

**Registration with checkbox and select props:**

```typescript
import { Checkbox, Select } from '@makeswift/runtime/controls'

runtime.registerComponent(
  lazy(() => import('./MyComponent')),
  {
    type: "my-component",
    label: "My Component",
    props: {
      showExtraContent: Checkbox({
        label: "Show Extra Content",
        defaultValue: true,
      }),
      layout: Select({
        label: "Layout",
        labelOrientation: "horizontal",
        options: [
          { value: "left-to-right", label: "Left to Right" },
          { value: "top-to-bottom", label: "Top to Bottom" },
        ],
        defaultValue: "left-to-right",
      }),
    },
  }
)
```

## The Style Control

**Registration example:**

```typescript
import { Style } from '@makeswift/runtime/controls'

runtime.registerComponent(
  lazy(() => import('./MyComponent')),
  {
    type: "my-component",
    label: "My Component",
    props: {
      className: Style({
        properties: Style.All,
      }),
    },
  }
)
```

**Style prop usage:**

```typescript
type Props = {
  className: string,
}

export const MyComponent = forwardRef(
  (
    { className }: Props,
    ref: Ref<HTMLDivElement>
  ) => {
    return (
      <div className={clsx(className, "w-full")} ref={ref}>
        <h1>Component</h1>
      </div>
    )
  }
)
```

## The RichText Control

**Registration example:**

```typescript
import { RichText } from '@makeswift/runtime/controls'

runtime.registerComponent(
  lazy(() => import('./MyComponent')),
  {
    type: "my-component",
    label: "My Component",
    props: {
      body: RichText({
        mode: RichText.Mode.Block,
      }),
    },
  }
)
```

**Rendering RichText props:**

```typescript
type Props = {
  body: ReactNode
}

export const MyComponent = forwardRef(
  (
    { body }: Props,
    ref: Ref<HTMLDivElement>
  ) => {
    return (
      <div ref={ref}>
        <h1>My Component</h1>
        <div>
          {body}
        </div>
      </div>
    )
  }
)
```

## The Slot Control

**Registration example:**

```typescript
import { Slot } from '@makeswift/runtime/controls'

import { runtime } from '@/lib/makeswift/runtime'

runtime.registerComponent(
  lazy(() => import('./MyComponent')),
  {
    type: "my-component",
    label: "My Component",
    props: {
      body: Slot(),
    },
  }
)
```

**Rendering Slot props:**

```typescript
type Props = {
  body: ReactNode
}

export const MyComponent = forwardRef(
  (
    { body }: Props,
    ref: Ref<HTMLDivElement>
  ) => {
    return (
      <div ref={ref}>
        <h1>My Component</h1>
        <div>
          {body}
        </div>
      </div>
    )
  }
)
```

## The Shape Control

**Registration example:**

```typescript
import { Checkbox, List, Shape, TextInput } from '@makeswift/runtime/controls'

runtime.registerComponent(
  lazy(() => import('./MyComponent')),
  {
    type: "my-component",
    label: "My Component",
    props: {
      items: List({
        label: "Items",
        type: Shape({
          type: {
            showItem: Checkbox({
              label: "Show Item",
              defaultValue: true,
            }),
            title: TextInput({
              label: "Title",
              defaultValue: "Enter title here",
            }),
          }
        }),
        getItemLabel(item) {
          return item?.title ?? "Item"
        },
      }),
    },
  }
)
```

[Next](./04_BuiltInElements.md)
