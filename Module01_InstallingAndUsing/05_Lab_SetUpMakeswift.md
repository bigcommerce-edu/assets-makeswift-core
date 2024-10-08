# Lab - Set Up Makeswift

## Install Catalyst

### Run the Installer

```shell
npm create @bigcommerce/catalyst@latest -- --integration=makeswift
```

### Run the Dev Server

```shell
cd /path/to/catalyst/project
npm run dev
```

## Connect Makeswift

**.env.local:**

```
MAKESWIFT_SITE_API_KEY={Makeswift API KEY}
```

## Examine the Local Installation

**Start the dev server:**

```shell
npm run dev
```

[Next](../Module02_MakeswiftArchitecture/01_ReactAndNextJs.md)