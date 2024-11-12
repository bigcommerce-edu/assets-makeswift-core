# Lab - Set Up Makeswift

## Install Catalyst

### Run the Installer

```shell
corepack enable pnpm
npm create @bigcommerce/catalyst@latest -- --gh-ref upstream/integrations/makeswift
```

### Run the Dev Server

```shell
cd /path/to/catalyst/project
pnpm run dev
```

## Connect Makeswift

**.env.local:**

```
MAKESWIFT_SITE_API_KEY={Makeswift API KEY}
```

## Examine the Local Installation

**Start the dev server:**

```shell
pnpm run dev
```

[Next](../Module02_MakeswiftArchitecture/01_ReactAndNextJs.md)