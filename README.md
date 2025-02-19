# Superchain Starter Kit

A lightweight, focused starting point for prototyping/building on the Superchain, featuring

- 🛠 [foundry](https://github.com/foundry-rs/foundry), [supersim](https://github.com/ethereum-optimism/supersim), [super-cli](https://github.com/ethereum-optimism/super-cli)
- 🎨 vite, tailwind-css, shadcn/ui, wagmi, viem
- [@eth-optimism/viem](https://github.com/ethereum-optimism/ecosystem/tree/main/packages/viem), [@eth-optimism/wagmi](https://github.com/ethereum-optimism/ecosystem/tree/main/packages/wagmi) - viem/wagmi extensions for the Superchain
- 💡 simple example app - CrossChainCounter

<img width="1007" alt="Screenshot 2025-02-17 at 8 09 02 PM" src="https://github.com/user-attachments/assets/af270104-9958-4e0b-8d1f-9b7c099143c9" />

### Looking for more advanced examples?

... WIP

## 🦬 Are you building at EthDenver 2025?

... WIP

## 🚀 Getting started

Get prototyping Superchain apps in under < 1 min! ❤️‍🔥

### 1. Create a new repository using this template:

Click the "Use this template" button above on GitHub, or [generate directly](https://github.com/new?template_name=superchain-starter&template_owner=ethereum-optimism)

### 2. Clone your new repository

```bash
git clone <your-new-repository-url>
cd superchain-starter
```

### 3. Install dependencies

```bash
pnpm i
```

### 4. Get started

```bash
pnpm dev
```

This command will:

- Start a local Superchain network (1 L1 chain and 2 L2 chains) using [supersim](https://github.com/ethereum-optimism/supersim)
- Launch the frontend development server at (http://localhost:5173)
- Deploy the smart contracts to your local network

Start building on the Superchain!

## Deploying contracts

The starter kit uses `super-cli` (or `sup`) to streamline contract deployment across the Superchain ecosystem. `sup` works great with Foundry projects while eliminating common multichain friction points:

- 🔄 **Foundry Compatible**: Seamlessly works with your existing Foundry setup and artifacts
- ⛓️ **Multi-Chain**: Deploy to multiple chains with a single command and pre-configured RPCs
- ⛽ **Gasless Deployments**: Instead of having to bridge to `n` chains
- 🎯 **Interactive mode**: No more complex command-line arguments

Alternatively, if you want to use Forge scripts directly, follow the multichain deployment example at [`contracts/script/Deploy.s.sol`](contracts/script/Deploy.s.sol)

### Deploying

Once you're ready to deploy, start `sup` in interactive mode

```bash
pnpm sup
```

Then you can follow the steps to deploy to supersim or the interop-alpha devnet

```bash
 Sup, what would you like to do on the Superchain today? ✨

 ❯ 🔄 Pick up where you left off: Deploy a contract
   🚀 Deploy a contract
   🌉 Bridge assets
```

```bash

🚀 Deploy Create2 Wizard

 ✓  Enter Foundry Project Path ./contracts/
 ✓  Select Contract CrossChainCounter.sol
 ✓  Configure Constructor Arguments
 ✓  Configure Salt ethers phoenix
 ✓  Select Network interop-alpha
 ✓  Select Chains interop-alpha-0, interop-alpha-1
 >  Verify Contract

Press ← to go back

 Do you want to verify the contract on the block explorer? Y/n

```

### Non-interactive mode

You can also skip the interactive mode entirely by passing the necessary arguments

```bash
pnpm sup deploy create2 --chains supersiml2a,supersiml2b --salt ethers phoenix --forge-artifact-path contracts/out/CrossChainCounter.sol/CrossChainCounter.json --network supersim --private-key 0x5de4111afa1a4b94908f83103eb1f1706367c2e68ca870fc3fb9a804cdab365a
```

### `--prepare` mode

To "prepare" a command without running it, run `sup` with the prepare mode. This will print the command instead of running it. Then you can run the prepared command directly to run immediately in non-interactive mode.

```bash
pnpm sup --prepare
```

### Make sure to build before deploying

`sup` assumes that your foundry project has already been built. Make sure to build before attempting to deploy

```
pnpm build:contracts
```

## 👀 Overview

### Example app

#### `CrossChainCounter` contract

- Simple `Hello world` for Superchain Interop
- Unlike the [single chain Counter](https://github.com/foundry-rs/foundry/blob/master/crates/forge/assets/CounterTemplate.sol), this one can only be incremented via cross-chain messages
- Learn more about this contract [here](./contracts/README.md)

#### Frontend for `CrossChainCounter`

- Simple frontend to interact with `CrossChainCounter`

### Tools

Superchain Starter kit is comprised of:

#### supersim

- local multichain environment that brings up 1 L1 chain and multiple L2 chains
- chains come with all of the [useful contracts](https://docs.optimism.io/app-developers/tutorials/supersim/chain-env/included-contracts) already deployed to replicate the Superchain environment

#### sup (super-cli)

- deploy & verify multichain contracts on the Superchain
- gasless, sponsored deploys (no funded wallet required for `interop-alpha`)
- interactive mode (no more juggling cli flags)
- seamless Foundry project compatibility - consumes Forge artifacts and emits standard broadcast outputs

#### foundry

- one of most popular Ethereum development toolchain
- blazing fast Ethereum toolchain to build & test smart contracts

#### wagmi / viem

- best in class typescript library for building onchain apps
- @eth-optimism/wagmi and @eth-optimism/viem adds useful extensions for interacting with Superchain apps

#### vite / tailwind / shadcn

- modern frontend tooling for fast, responsive UI development

## 📁 Directory structure

This starter kit is organized to get you building on the Superchain as quickly as possible. The repository combines smart contracts and a frontend in a single repo. Solidity code goes in `/contracts`, and the typescript frontend goes in `/src`

```
superchain-starter/
├── contracts/                   # Smart contract code
│   ├── src/                    # Contract source files
│   │   └── ui/                # UI components
│   ├── test/                   # Contract test files
│   ├── script/                 # Forge scripts
│   ├── lib/                    # Contract dependencies
│   └── foundry.toml           # Foundry configuration
├── src/                        # Frontend source code
│   ├── components/             # React components
│   │   └── ui/                # UI components
│   ├── abi/                    # Contract ABIs
│   ├── lib/                    # Frontend utilities
│   ├── App.tsx                # Main application component
│   ├── Providers.tsx          # Application providers
│   └── main.tsx               # Application entry point
├── public/                     # Static assets for the frontend
├── supersim-logs/             # Local network logs
├── package.json               # Project dependencies and scripts
├── mprocs.yaml               # Development process manager config
└── README.md                 # Project documentation
```

### A note on project structure

While this structure is great for getting started and building proof of concepts, it's worth noting that many production applications eventually migrate to separate repositories for contracts and frontend code.

For reference, here are some examples of this separation in production applications:

- Uniswap: [Uniswap contracts](https://github.com/Uniswap/v4-core), [Uniswap frontend](https://github.com/Uniswap/interface)
- Across: [Across contracts](https://github.com/across-protocol/contracts), [Across frontend](https://github.com/across-protocol/frontend)
- Farcaster: [Farcaster contracts](https://github.com/farcasterxyz/contracts)

## ⚖️ License

Files are licensed under the [MIT license](./LICENSE).

<a href="./LICENSE"><img src="https://user-images.githubusercontent.com/35039927/231030761-66f5ce58-a4e9-4695-b1fe-255b1bceac92.png" alt="License information" width="200" /></a>
This project is a demonstration of blockchain technology and smart contract integration.