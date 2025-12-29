# Theming in Catalyst

## Try Out a New Property

Try adding a new style property of your own in the "Product Card" group.

1. **Open** the file _lib/makeswift/components/site-theme/components/product-card.ts_ and **add** the _titleSize_ prop to the _props_ object.


```js {6-10} copy
export const productCard = Group({
  label: 'Product card',
  preferredLayout: Group.Layout.Popover,
  props: {
    ...
    titleSize: Number({
      label: 'Title font size',
      suffix: 'px',
      defaultValue: 20,
    }),
  },
});
```

Since you've added this within an existing group, this is all that's required in order for your new property to show up in the "Site Theme" element properties in the Makeswift builder.

![The new font size property](https://storage.googleapis.com/bigcommerce-production-dev-center/learning-edu/makeswift-core/site-theme-new-size-prop.png)


Given the existing group name and the transformation of our _titleSize_ prop name to kebab casing, we can expect this value to be output for the CSS variable _--product-card-title-size_.

2. In the root directory of your Catalyst theme components, **edit** the file _primitives/product-card/index.tsx_ and **add** a _style_ prop to the _&lt;span&gt;_ where _\{title\}_ is rendered.


```jsx {7-9} copy
<Link ...>
  <span
    className={clsx(
      ...
    )}

    style={{
      'fontSize': 'var(--product-card-title-size, 20px)',
    }}
  >
    {title}
  </span>
  ...
```

3. In the location bar of the Makeswift builder, **enter** the URL path of a valid category page.
4. **Select** the "Site Theme" element in the Elements panel and try **editing** the new "Title font size" property. **Observe** the effects on the cards in the product list.
