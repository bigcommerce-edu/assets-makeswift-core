# Installing with Catalyst

## The Installation Process

```shell
npm create @bigcommerce/catalyst@latest -- --gh-ref upstream/integrations/makeswift
```

## Connecting a BigCommerce Store

```shell
npx @bigcommerce/create-catalyst@latest init
```

## Connecting a Makeswift Site

**.env.local:**

```
MAKESWIFT_SITE_API_KEY={Makeswift API KEY}
```

[Next](./04_UsingTheMakeswiftInstaller.md)
