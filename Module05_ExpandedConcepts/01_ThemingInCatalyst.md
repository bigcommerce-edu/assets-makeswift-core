# Theming in Catalyst

## Try Out a New Property

**Add to `lib/makeswift/components/site-theme/components/product-card.ts`:**

```typescript
export const productCard = Group({
  label: 'Product card',
  preferredLayout: Group.Layout.Popover,
  props: {
    ...
    // START NEW CODE
    titleSize: Number({
      label: 'Title font size',
      suffix: 'px',
      defaultValue: 20,
    }),
    // END NEW CODE
  },
});
```

**Edit in theme `primitives/product-card/index.tsx`:**

```typescript
<Link ...>
  <span
    className={clsx(
      ...
    )}

    {/* START NEW CODE */}
    style={{
      'fontSize': 'var(--product-card-title-size, 20px)',
    }}
    {/* END NEW CODE */}
  >
    {title}
  </span>
  ...
```

[Next](./04_BuiltInElements.md)
