# Built-in Elements

## Using MakeswiftComponent

**Example component:**

```javascript
import { Color, Slot } from "@makeswift/runtime/controls";
import { runtime } from '~/lib/makeswift/runtime';

const FancyBox = (
  {
    highlightColor,
    content
  }: {
    highlightColor: string,
    content: ReactNode
  }
) => {
  return (
    <div ...>
      <div className="border border-solid border-grey p-8">
        <h1 className="bold text-2xl font-heading">
          FancyBox Content
        </h1>
        {content}
      </div>
    </div>
  );
};

runtime.registerComponent(FancyBox, {
  type: 'fancy-box',
  label: 'Fancy Box',
  props: {
    highlightColor: Color({
      label: 'Highlight color',
      defaultValue: 'red',
    }),
    content: Slot(),
  },
});
```

**Used as a built-in element:**

```javascript
import { MakeswiftComponent } from '@makeswift/runtime/next';
import { getComponentSnapshot } from '~/lib/makeswift/client';

const MyPage = async () => {
  const snapshot = await getComponentSnapshot('global-fancy-box');

  return (
    <section ...>
      <div ...>
        <div>Non-editable component page content</div>
      </div>
      <div>
        <MakeswiftComponent
          label="Global Fancy Box"
          snapshot={snapshot}
          type="fancy-box"
          />
      </div>
    </section>
  );
};
```

**Using a dynamic identifier:**

```javascript
const MyPage = async () => {
  const snapshot = await getComponentSnapshot(`fancy-box-`${article.id});

  return (
    <main>
      ...
        <MakeswiftComponent
          label={`Fancy Box for ${article.title}`}
          snapshot={snapshot}
          ...
         />
      ...
  );
};
```

**Using the _hidden_ property:**

```javascript
runtime.registerComponent(FancyBox, {
  type: 'fancy-box,
  hidden: true,
  ...
});
```

**The wrapper component:**

```typescript
import { Component } from '~/lib/makeswift/component';

...

const MyPage = async () => {
  return (
    <section ...>
      <div ...>
        <div>Non-editable component page content</div>
      </div>
      <div>
        <Component
          label="Global Fancy Box"
          snapshotId='global-fancy-box'
          type="fancy-box"
        />
      </div>
    </section>
  );
};
```

## Editable Regions with Slot

**Editable region example:**

```typescript
import { Slot } from '@makeswift/runtime/next';
import { getComponentSnapshot } from '~/lib/makeswift/client';

...

const MyPage = async () => {
  const regionSnapshot = await getComponentSnapshot('my-region');

  return (
    <section ...>
      ...
      <Slot fallback={<div>Fallback for slot ...</div>}
        label="My Region" 
        snapshot={regionSnapshot}
      />
    </section>
  );
};
```

## Mixing Prop Sources

**Multiple registrations with hard-coded props:**

```javascript
runtime.registerComponent((propsFromControls) => {
    return (
      <FancyBox 
        borderColor="#ccc" 
        {...propsFromControls} 
      />
    );
  }, {
  type: 'fancy-box-light',
  label: 'Fancy Box Light (hidden)',
  hidden: true,
  props: {
    className: Style({ properties: Style.All }),
    extraContent: Slot(),
  },
});

runtime.registerComponent((propsFromControls) => {
    return (
      <FancyBox 
        borderColor="#333" 
        {...propsFromControls} 
      />
    );
  }, {
  type: 'fancy-box-dark',
  label: 'Fancy Box Dark (hidden)',
  hidden: true,
  props: {
    className: Style({ properties: Style.All }),
    extraContent: Slot(),
  },
});
```

### Data from Server Components

**Example component:**

```javascript
const FancyBox = (
  {
    className,
    borderColor,
    cards,
    extraContent
  }: {
    className?: string,
    borderColor?: string,
    cards?: {title?: string, content?: string}[],
    extraContent: ReactNode
  }
) => {
  return (
    <>
      ...
    </>
  );
};
```

**Example intermediary component:**

```javascript
import React, { createContext, useContext } from 'react';

const FancyBoxContext = createContext<
  { cards: {title: string, content: string}[] } | null
>(null);
export const FancyBoxContextProvider = (
  {
    value,
  }: {
    value: { cards: {title: string, content: string}[] } | null,
  }
) => {
  return <FancyBoxContext.Provider value={value} />;
};

export const MakeswiftFancyBox = (
  {
    className,
    borderColor,
    extraContent
  }: {
    className?: string,
    borderColor?: string,
    extraContent: ReactNode
  }
) => {
  const context = useContext(FancyBoxContext);
  const cards = context?.cards ?? [];

  return (
    <FancyBox 
      className={className} 
      borderColor={borderColor}
      cards={cards}
      extraContent={extraContent} />
  );
};
```

**Intermediary component registration:**

```javascript
runtime.registerComponent(MakeswiftFancyBox, {
  type: 'fancy-box-element',
  label: 'Fancy Box (private)',
  hidden: true,
  props: {
    className: Style({ properties: Style.All }),
    borderColor: Color({ label: "Border Color" }),
    extraContent: Slot(),
  },
});
```

**Creating the built-in element:**

```javascript
const MyPage = async () => {
  const snapshot = await getComponentSnapshot(`fancy-box-${id}`);
  const cards = // Fetch cards from elsewhere

  return (
    <>
      <FancyBoxContextProvider value={{ cards }}>
        <MakeswiftComponent
          label={`Fancy Box for ${id}`}
          snapshot={snapshot}
          type='fancy-box-element'
         />
      </FancyBoxContextProvider>
    </>
  );
};
```
