---
sidebar_label: "Enable Fiat On Ramp"
sidebar_position: 5
custom_edit_url: https://github.com/bcnmy/docs/blob/master/docs/Account/fiatonramp.md
---

# Enable Fiat On-Ramp

BiconomySDK's Transak library is made for developers who just want on-ramp solutions and don't want to go through with all the steps to integrate the SDK.

It is a typescript wrapper on `transak.js` SDK which abstracts a few steps for the developers and users.

## Steps to Enable Fiat On-Ramp

- Import the `@biconomy-devx/transak` package into your project.

```js
import Transak from "@biconomy-devx/transak";
```

- Initialize the project without going to any dashboard

```js
// init the widget
const transak = new Transak("STAGING");
transak.init();
```

- If you are using Fiat On Ramp then you can directly pass in the email like so:

```js
import Transak from "@biconomy-devx/transak";

// use this info for transak package
const transak = new Transak("STAGING", {
  walletAddress: userAddress,
  userData: {
    firstName: userInfo?.name || "",
    email: userInfo?.email || "",
  },
});
transak.init();
```

- On `transak.init()` Transak widget opens and users can buy on-ramp.

## Code Examples

- https://github.com/bcnmy/sdk-demo
- https://github.com/bcnmy/hyphen-ui/tree/demo-sdk

:::info
If you have any questions please post them on the [Biconomy SDK Forum](https://forum.biconomy.io/)
:::
