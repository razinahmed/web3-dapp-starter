<div align="center">

# 🌐 Web3 dApp Starter Kit

<img src="https://placehold.co/900x250/1e1e2e/8b5cf6.png?text=Next.js+%7C+Hardhat+%7C+Solidity+%7C+Web3Modal" alt="Web3 dApp Starter Banner" />

<br/>

**The fastest way to build, test, and deploy decentralized applications (dApps) on Ethereum, Polygon, and EVM-compatible blockchains — powered by Next.js 14, Hardhat, and Web3Modal.**

[![Next.js](https://img.shields.io/badge/Next.js-14-000000?style=for-the-badge&logo=next.js&logoColor=white)](https://nextjs.org/)
[![Solidity](https://img.shields.io/badge/Solidity-0.8.20+-363636?style=for-the-badge&logo=solidity&logoColor=white)](https://soliditylang.org/)
[![Hardhat](https://img.shields.io/badge/Hardhat-2.x-FFF100?style=for-the-badge&logo=hardhat&logoColor=black)](https://hardhat.org/)
[![Ethereum](https://img.shields.io/badge/Ethereum-3C3C3D?style=for-the-badge&logo=ethereum&logoColor=white)](https://ethereum.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-8b5cf6?style=for-the-badge)](LICENSE)

[Features](#-features) · [Quick Start](#-quick-start) · [Smart Contracts](#-smart-contracts) · [Deployment](#-deployment-guide) · [Contributing](#-contributing)

</div>

---

## 📋 Table of Contents

- [About](#-about)
- [Features](#-features)
- [Smart Contracts](#-smart-contracts)
- [Quick Start](#-quick-start)
- [MetaMask Integration](#-metamask-integration)
- [Hardhat Commands](#-hardhat-commands)
- [Deployment Guide](#-deployment-guide)
- [Environment Variables](#-environment-variables)
- [Project Structure](#-project-structure)
- [Tech Stack](#-tech-stack)
- [Supported Networks](#-supported-networks)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🔍 About

**Web3 dApp Starter Kit** is a full-stack boilerplate for building **decentralized applications** on Ethereum and EVM-compatible chains. It combines a modern **Next.js 14** frontend with a **Hardhat** smart contract development environment, connected through **wagmi** and **viem** for type-safe blockchain interactions. Whether you are building a DeFi protocol, an NFT marketplace, or a DAO voting system, this starter kit gives you a production-ready foundation.

---

## ✨ Features

| Feature | Description |
|---|---|
| **Next.js 14 App Router** | Server components, streaming SSR, and optimized performance |
| **Hardhat Development** | Local blockchain, automated testing, and deployment scripts |
| **Web3Modal v3** | Beautiful wallet connection modal supporting 300+ wallets |
| **wagmi + viem** | Type-safe React hooks for Ethereum interactions |
| **TypeChain** | Auto-generated TypeScript bindings for smart contracts |
| **Tailwind CSS + shadcn/ui** | Responsive, accessible UI components |
| **Multi-Chain** | Deploy to Ethereum, Polygon, Arbitrum, Optimism, Base |
| **Contract Verification** | Automated Etherscan/Polygonscan contract verification |
| **Gas Optimization** | Hardhat Gas Reporter for tracking deployment costs |
| **Test Coverage** | Solidity coverage reports with `solidity-coverage` |

---

## 📜 Smart Contracts

### Included Contracts

| Contract | Purpose | Features |
|---|---|---|
| **`SimpleStorage.sol`** | Example starter contract | Store/retrieve values, event emission, owner-only functions |
| **`Token.sol`** | ERC-20 token template | Mintable, burnable, pausable with OpenZeppelin |
| **`NFT.sol`** | ERC-721 NFT template | Metadata URI, royalties (EIP-2981), whitelist minting |

### Contract Architecture

```solidity
// SimpleStorage.sol — Example
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract SimpleStorage {
    uint256 private value;
    address public owner;

    event ValueChanged(uint256 newValue, address indexed changedBy);

    modifier onlyOwner() {
        require(msg.sender == owner, "Not the owner");
        _;
    }

    constructor() {
        owner = msg.sender;
    }

    function store(uint256 _value) public onlyOwner {
        value = _value;
        emit ValueChanged(_value, msg.sender);
    }

    function retrieve() public view returns (uint256) {
        return value;
    }
}
```

### Testing Contracts

```bash
cd contracts

# Run all tests
npx hardhat test

# Run with gas reporting
REPORT_GAS=true npx hardhat test

# Generate coverage report
npx hardhat coverage
```

---

## 🚀 Quick Start

### Prerequisites

- Node.js 18.17 or higher
- [MetaMask](https://metamask.io/) browser extension
- npm, yarn, or pnpm

### 1. Clone the Repository

```bash
git clone https://github.com/razinahmed/web3-dapp-starter.git
cd web3-dapp-starter
```

### 2. Set Up Smart Contracts

```bash
cd contracts
npm install

# Start a local Hardhat node
npx hardhat node
```

### 3. Deploy Contracts (New Terminal)

```bash
cd contracts
npx hardhat run scripts/deploy.js --network localhost
```

### 4. Start the Frontend

```bash
cd frontend
npm install
npm run dev
```

Open `http://localhost:3000` to see your dApp. Connect MetaMask to interact with the deployed contracts.

---

## 🦊 MetaMask Integration

### Connecting to Local Hardhat Network

1. Open MetaMask and click **Add Network**
2. Enter the following details:

| Field | Value |
|---|---|
| Network Name | Hardhat Local |
| RPC URL | `http://127.0.0.1:8545` |
| Chain ID | `31337` |
| Currency Symbol | ETH |

3. Import a test account using one of Hardhat's private keys (printed when you run `npx hardhat node`)

### Wallet Connection Flow

The starter kit uses **Web3Modal v3** which supports:

- MetaMask
- WalletConnect (300+ mobile wallets)
- Coinbase Wallet
- Rainbow
- Trust Wallet
- And many more

```tsx
// Already configured in frontend/src/lib/web3modal.ts
import { createWeb3Modal, defaultWagmiConfig } from '@web3modal/wagmi/react'

// Usage in any component
import { useAccount, useConnect } from 'wagmi'

export function ConnectButton() {
  const { address, isConnected } = useAccount()
  // Web3Modal handles the rest
}
```

---

## 🔨 Hardhat Commands

| Command | Description |
|---|---|
| `npx hardhat compile` | Compile all Solidity contracts |
| `npx hardhat test` | Run the test suite |
| `npx hardhat node` | Start a local blockchain node |
| `npx hardhat run scripts/deploy.js --network localhost` | Deploy to local node |
| `npx hardhat run scripts/deploy.js --network sepolia` | Deploy to Sepolia testnet |
| `npx hardhat run scripts/deploy.js --network mainnet` | Deploy to Ethereum mainnet |
| `npx hardhat verify --network sepolia <CONTRACT_ADDRESS>` | Verify on Etherscan |
| `REPORT_GAS=true npx hardhat test` | Run tests with gas reporting |
| `npx hardhat coverage` | Generate test coverage report |
| `npx hardhat clean` | Clear cache and artifacts |
| `npx hardhat typechain` | Generate TypeScript bindings |

---

## 🚢 Deployment Guide

### Step 1: Deploy to Testnet (Sepolia)

```bash
# Make sure your .env has SEPOLIA_RPC_URL and PRIVATE_KEY
cd contracts
npx hardhat run scripts/deploy.js --network sepolia
```

### Step 2: Verify the Contract

```bash
npx hardhat verify --network sepolia <DEPLOYED_CONTRACT_ADDRESS> <CONSTRUCTOR_ARGS>
```

### Step 3: Deploy to Mainnet

> [!WARNING]
> Deploying to mainnet uses real ETH. Double-check your contract code and run a full audit before deploying.

```bash
npx hardhat run scripts/deploy.js --network mainnet
npx hardhat verify --network mainnet <DEPLOYED_CONTRACT_ADDRESS>
```

### Step 4: Deploy the Frontend

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/razinahmed/web3-dapp-starter)

Update `NEXT_PUBLIC_CONTRACT_ADDRESS` in your Vercel environment variables with the deployed contract address.

### Deployment Checklist

- [ ] All tests passing (`npx hardhat test`)
- [ ] Gas costs reviewed (`REPORT_GAS=true npx hardhat test`)
- [ ] Contract verified on block explorer
- [ ] Frontend environment variables updated with mainnet contract addresses
- [ ] MetaMask network switched to correct chain
- [ ] Consider a professional smart contract audit for production dApps

---

## 🔐 Environment Variables

### Contracts (`contracts/.env`)

| Variable | Required | Description |
|---|:-:|---|
| `PRIVATE_KEY` | ✅ | Deployer wallet private key (without 0x prefix) |
| `SEPOLIA_RPC_URL` | ✅ | Alchemy/Infura Sepolia RPC endpoint |
| `MAINNET_RPC_URL` | ❌ | Alchemy/Infura Mainnet RPC endpoint |
| `ETHERSCAN_API_KEY` | ❌ | Etherscan API key for contract verification |
| `POLYGONSCAN_API_KEY` | ❌ | Polygonscan API key for Polygon deployments |
| `REPORT_GAS` | ❌ | Enable gas reporting in tests |

### Frontend (`frontend/.env.local`)

| Variable | Required | Description |
|---|:-:|---|
| `NEXT_PUBLIC_CONTRACT_ADDRESS` | ✅ | Deployed smart contract address |
| `NEXT_PUBLIC_WALLETCONNECT_PROJECT_ID` | ✅ | WalletConnect Cloud project ID |
| `NEXT_PUBLIC_CHAIN_ID` | ❌ | Target chain ID (default: 1 for mainnet) |

---

## 📁 Project Structure

```
web3-dapp-starter/
├── contracts/                      # Hardhat smart contract project
│   ├── contracts/                  # Solidity source files
│   │   ├── SimpleStorage.sol       # Example storage contract
│   │   ├── Token.sol               # ERC-20 token template
│   │   └── NFT.sol                 # ERC-721 NFT template
│   ├── scripts/
│   │   └── deploy.js               # Deployment scripts
│   ├── test/                       # Contract test files
│   ├── hardhat.config.js           # Hardhat configuration
│   └── package.json
├── frontend/                       # Next.js frontend application
│   ├── src/
│   │   ├── app/                    # App Router pages
│   │   ├── components/             # React components
│   │   ├── hooks/                  # Custom wagmi hooks
│   │   ├── lib/                    # Web3Modal config, utils
│   │   └── abi/                    # Contract ABIs (auto-generated)
│   ├── public/                     # Static assets
│   ├── tailwind.config.ts
│   └── package.json
├── LICENSE
└── README.md
```

---

## 🛠️ Tech Stack

| Category | Technologies |
|---|---|
| **Frontend** | Next.js 14, React 18, TypeScript |
| **Styling** | Tailwind CSS, shadcn/ui |
| **Web3 Client** | wagmi, viem, Web3Modal v3 |
| **Smart Contracts** | Solidity 0.8.20+, OpenZeppelin Contracts |
| **Dev Environment** | Hardhat, TypeChain, Ethers.js v6 |
| **Testing** | Chai, Mocha, Hardhat Test, solidity-coverage |
| **Deployment** | Vercel (frontend), Hardhat Deploy (contracts) |

---

## 🌐 Supported Networks

| Network | Chain ID | Type | Explorer |
|---|:-:|---|---|
| Ethereum Mainnet | 1 | Production | [etherscan.io](https://etherscan.io) |
| Sepolia Testnet | 11155111 | Testnet | [sepolia.etherscan.io](https://sepolia.etherscan.io) |
| Polygon Mainnet | 137 | Production | [polygonscan.com](https://polygonscan.com) |
| Polygon Mumbai | 80001 | Testnet | [mumbai.polygonscan.com](https://mumbai.polygonscan.com) |
| Arbitrum One | 42161 | Production | [arbiscan.io](https://arbiscan.io) |
| Optimism | 10 | Production | [optimistic.etherscan.io](https://optimistic.etherscan.io) |
| Base | 8453 | Production | [basescan.org](https://basescan.org) |
| Hardhat Local | 31337 | Development | N/A |

---

## 🤝 Contributing

Contributions are welcome! Here is how to get involved:

1. **Fork** this repository
2. **Create** a feature branch (`git checkout -b feature/new-contract`)
3. **Write** tests for any new smart contracts
4. **Ensure** all tests pass (`npx hardhat test`)
5. **Submit** a Pull Request

Ideas for contributions:
- Additional contract templates (DAO, Marketplace, Staking)
- Multi-chain deployment scripts
- Subgraph integration (The Graph)
- IPFS metadata upload utilities

---

## 📄 License

This project is licensed under the **MIT License** — free to use for commercial projects. See the [LICENSE](LICENSE) file for details.

---

<div align="center">

**Built by [Razin Ahmed](https://github.com/razinahmed)**

If this starter kit helped you launch your dApp faster, please give the repo a ⭐

<img src="https://komarev.com/ghpvc/?username=razinahmed&style=flat-square&color=8b5cf6&label=REPO+VIEWS" alt="Repo Views" />

</div>
