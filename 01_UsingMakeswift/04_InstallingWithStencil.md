# Installing with Stencil

**Makeswift on Stencil is currently in Beta.** Features and availability are subject to change.

Unlike Catalyst, a Stencil storefront must opt in to the Makeswift editing experience before it can be provisioned:

1. Opt the store into the Makeswift on Stencil Beta.
2. In Channel Manager, view the Stencil storefront channel.
3. Select **Edit in Makeswift** on the channel entry. The first selection creates and connects a Makeswift site for the channel, then opens the editor.

No CLI install step is required — provisioning happens entirely through the control panel/channel UI.

Key facts for this integration:

* Custom React components are not supported on Stencil (to be supported at a later date). Editing is limited to Makeswift's built-in controls and BigCommerce-provided components.
* The integration ships its own set of Stencil-specific components (e.g. products, product lists) that render with the theme's own markup/styling.
* Under the hood: a BigCommerce back-end proxy service renders the page HTML with the appropriate renderer, detects the theme's regions, and injects React tooling into those regions before the HTML reaches the browser — which is what makes a non-React, Handlebars-based storefront editable in Makeswift.
