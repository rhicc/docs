---
sidebar_label: "Particle Network"
sidebar_position: 3
---

# Particle Network

One way to utilize Social Logins is via Particle Network. This section will give you code snippets for creating Biconomy Smart Accounts with Particle Network. Particle Network allows you to introduce familiar Web2 experiences, with the following code snippets you can unlock: authentication with email to create a smart account as well as authentication with different social providers to create a Smart Account.

:::tip

Check out an end-to-end integration of Particle with Biconomy on this [example app](https://aaparticle.vercel.app/) and [repo](https://github.com/bcnmy/biconomy_particle_example)!

:::

## Dependencies

You will need the following dependencies to create a Smart Account this way:

```bash
yarn add @biconomy-devx/account @biconomy-devx/particle-auth ethers@5.7.2
```

## Imports

```typescript
import { createSmartAccountClient, LightSigner } from "@biconomy-devx/account";
import { Wallet, providers, ethers } from "ethers";
import {
  ParticleAuthModule,
  ParticleProvider,
} from "@biconomy-devx/particle-auth";
```

## Particle Auth Configuration

Particle auth will require api keys which you can get from the [Particle Dashboard](https://docs.particle.network/getting-started/dashboard).

```typescript
const particle = new ParticleAuthModule.ParticleNetwork({
  projectId: "",
  clientKey: "",
  appId: "",
  wallet: {
    displayWalletEntry: true,
    defaultWalletEntryPosition: ParticleAuthModule.WalletEntryPosition.BR,
  },
});
```

## Create the Biconomy Smart Account

```typescript
const connect = async () => {
  try {
    const userInfo = await particle.auth.login();
    console.log("Logged in user:", userInfo);
    const particleProvider = new ParticleProvider(particle.auth);
    const web3Provider = new ethers.providers.Web3Provider(
      particleProvider,
      "any"
    );

    const smartAccount = await createSmartAccountClient({
      signer: web3Provider.getSigner() as LightSigner,
      bundlerUrl:
        "https://bundler.biconomy.io/api/v2/{chain-id-here}/nJPK7B3ru.dd7f7861-190d-41bd-af80-6877f74b8f44",
      biconomyPaymasterApiKey: "https://docs.biconomy.io/dashboard/paymaster", // <-- Read about this here
    });

    const address = await smartAccount.getAccountAddress();
  } catch (error) {
    console.error(error);
  }
};
```
