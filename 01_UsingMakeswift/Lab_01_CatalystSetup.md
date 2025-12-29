# Lab - Set Up Catalyst and Makeswift

Note that the starter codebase for these labs picks up where the labs from Catalyst Core left off. If you have a local project as set up in these labs, you can skip this lab and simply start the dev server in your existing example project:

```shell
pnpm run dev
```

**Prerequisites**

* A BigCommerce [sandbox store](https://developer.bigcommerce.com/docs/start/about/sandboxes) or [trial store](https://www.bigcommerce.com/essentials/), or a full production store, with an available storefront seat
* A control panel user with the following permissions: "Create Store-level API accounts," "Install applications," "Launch applications," "Create Channels" ([Learn about high-risk permissions](https://support.bigcommerce.com/s/article/User-Permissions#highrisk))
* A command-line interface on your local machine
* Node.js 20 or later ([nvm](https://github.com/nvm-sh/nvm) recommended)
* The [pnpm](https://pnpm.io/installation) package manager
* [Git CLI](https://git-scm.com/)


For following along in the code in future lessons, it's also helpful to make sure you have a code editor, like [VS Code](https://code.visualstudio.com/), to open your Catalyst project once installed.

If you run into an error related to your maximum number of active storefronts during the Catalyst CLI installation, this means you do not have sufficient storefront seats.

In Channel Manager (or Channels) in your store control panel, you will need to either delete/deactivate a channel, "Add new" and confirm/update all requirements for multi-storefront if you haven't previously done so, or else use a different sandbox store with an available seat.

## Step 1: Create a Catalyst Storefront

1. **Log into** your BigCommerce store control panel.
2. **Navigate** to Channel Manager (or Channels) and **Create channel**.
3. In the list of channel types, **choose** "Create" next to the "Catalyst" type.
4. **Enter** a storefront name, **select** "Use sample data," and **click** "Create" to finalize the storefront.


Once the provisioning process is begun, you will need to wait for the initial deployment to complete.

![A Catalyst deployment in progress](https://storage.googleapis.com/bigcommerce-production-dev-center/learning-edu/catalyst-core/catalyst-channel-in-progress.png)

Proceed with the following steps after deployment is complete.

5. **Click** the "View storefront" button to view your hosted preview storefront.
6. **Click** the "Edit in Makeswift" button to launch the Makeswift editor and **confirm** that you are able to edit your pages.

Note that you can return to the storefront overview page at any time by navigating to Channel Manager (or Channels) in your control panel and clicking on the Catalyst storefront channel.

## Step 2: Install the Catalyst Project

Rather than start your custom code from scratch, you’ll be starting from a Catalyst codebase that already has certain boilerplate in place, in preparation for subsequent labs.

1. **Run** the following command, replacing the path to the working directory with your own path.


```bash copy
corepack enable pnpm && pnpm dlx create-next-app@latest -e https://github.com/bigcommerce-edu/lab-catalyst-makeswift-faqs/tree/e-makeswift-start /path/to/working/directory
```

**Troubleshooting**

_The pnpm command is unrecognized._

In some environments where file permissions are highly restricted, you may need to prepend `corepack` to the use of `pnpm` commands (for example, `corepack pnpm dlx create-next-app@latest ...`)

_I receive interactive prompts._

The standard interactive flow for creating a new Next.js app will be initiated if the `-e` option isn’t recognized to provision from an existing “example” project. A brand new Next.js project isn’t what we’re after, so try manually cloning the starting state of the project repo:

```bash copy
git clone --branch e-catalyst-start git@github.com:bigcommerce-edu/lab-catalyst-makeswift-faqs.git /path/to/working/directory
cd /path/to/working/directory
pnpm install
```

2. **Run** the following commands.

```bash copy
cd /path/to/working/directory
pnpm dlx @bigcommerce/create-catalyst@1.0.1 init
```

You will eventually be presented with the BigCommerce device authorization URL - `https://login.bigcommerce.com/device/connect` - and a unique code.

3. **Press Enter** or manually **browse** to the given URL and **log into** your BigCommerce account.
4. If you have multiple stores associated with your account, **choose** the store you want to associate with your Catalyst project.
5. **Enter** the code from your command line output, and **click** "Next."
6. **Allow** the required permissions.

With authorization completed, back at the command line, there will be new installation steps to complete.

7. **Respond** to the prompt "Would you like to create a new channel?" with "No."
8. **Select** the storefront channel you previously created in the control panel.

The completion of the installation may take a few minutes. The installer will install the Catalyst code files into your local project, install all `npm` dependencies, and configure your store information and credentials.

## Step 3: Run the Dev Server

1. **Navigate** to the new project working directory.

```bash copy
cd /path/to/catalyst/project
```

2. **Run** the dev server.

```bash copy
pnpm run dev
```

3. **Browse** to the URL displayed in the command line output. (Usually `http://localhost:3000`)


Provided that you chose to install sample data when creating your Catalyst storefront, you should see a fully populated storefront home page. Your local site should be nearly identical to your hosted preview environment, although as previously noted, there may be differences between the installed codebase and the deployed preview.

![Example of a fresh local site](https://storage.googleapis.com/bigcommerce-production-dev-center/learning-edu/catalyst-core/catalyst-fresh-home.jpg)


4. If you are not still logged in the Makeswift editor, **return** to Channel Manager (or Channels) in your BigCommerce control panel, **click** on your storefront channel, and **click** "Edit in Makeswift."
5. In the Makeswift editor, **use** the site switcher in the upper left corner to **switch** to the "Dev" site (for example, "My Catalyst Storefront (Dev)") and **confirm** that the `localhost` site successfully loads in the editor.


**Troubleshooting**

If you encounter an error while starting the dev server related to an issue finding a matching `keyid`, you may need to upgrade a pre-existing `corepack` version.

```bash
npm install -g corepack@latest
```

## Step 4: Examine the Local Configuration

1. **Open** the file `.env.local` in your new project and **observe** the environment variables that have been created by the installer.

| Variable | Description |
| --- | --- |
| `AUTH_SECRET` | A secret value used for Auth.js authenticated session management |
| `BIGCOMMERCE_STORE_HASH` | The hash of the BigCommerce store this project is connected to |
| `BIGCOMMERCE_CHANNEL_ID` | The ID of the new storefront channel that was created in your store. This new channel has the type "storefront" and the platform "catalyst". |
| `BIGCOMMERCE_STOREFRONT_TOKEN` | This GraphQL Storefront API token that Catalyst uses for its interactions with the BigCommerce platform. |
| `ENABLE_ADMIN_ROUTE` | Enables the convenience URL path */admin* on the storefront, which will direct you to your store's control panel&nbsp; |
| `TURBO_REMOTE_CACHE_SIGNATURE_KEY` | A key related to Turborepo, a tool used by Catalyst for optimizing building within the monorepo |
| `MAKESWIFT_SITE_API_KEY` | The API key of the Makeswift dev site |

2. **Browse** to the file `.catalyst` in your project and **observe** the variables created here.

| Variable | Description |
| --- | --- |
| `storeHash` | The same store hash stored in `.env.local` |
| `accessToken` | A BigCommerce REST API token generated during the device auth flow |

Unlike the values in `.env.local`, the values in `.catalyst` are only used by the CLI installer, not by the storefront application itself, and so these values do not correspond to any environment configuration that must be set up in deployment environments.

3. **Browse** to the `/admin` path on your local storefront to visit your BigCommerce control panel.

## The Local Dev Server and Cache

At various points while working in your local project, you may need to restart your dev server or clear the Next.js or Turborepo caches. Below is an example set of steps to do all three.

1. **Stop** the local dev server (CTRL-C at the command line).
2. **Clear** the contents of the Next.js cache directory. This is located at `core/.next/cache` in your project working directory.
3. **Clear** the contents of the Turborepo cache directory. This is located at `.turbo/cache` in your project working directory.
4. **Start** the dev server again.

```bash copy
pnpm run dev
```

Make sure only to clear a given cache when necessary. It is generally not necessary to clear the Turborepo cache to make sure your storefront content is up to date.
