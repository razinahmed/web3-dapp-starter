# 🌐 Web3 dApp Starter Kit

<div align="center">

<img src="https://placehold.co/800x200/1e1e2e/8b5cf6?text=Next.js+%2B+Hardhat+%2B+Web3Modal" alt="Web3 Banner" />

**The fastest way to build, test, and deploy decentralized applications (dApps) on Ethereum & Polygon.**

[![Next.js](https://img.shields.io/badge/next.js-14-black.svg?style=for-the-badge&logo=next.js&logoColor=white)](https://nextjs.org/)
[![Solidity](https://img.shields.io/badge/Solidity-%23363636.svg?style=for-the-badge&logo=solidity&logoColor=white)](https://soliditylang.org/)
[![Hardhat](https://img.shields.io/badge/Hardhat-FFF100.svg?style=for-the-badge&logo=hardhat&logoColor=black)](https://hardhat.org/)

</div>

---

## ⚡ Features

This boilerplate combines the absolute best tools in the modern Web3 stack:

- **Frontend:** Next.js 14 App Router, Tailwind CSS, shadcn/ui.
- **Web3 Integrations:** `wagmi`, `viem`, and `Web3Modal` for seamless wallet connections.
- **Smart Contracts:** Hardhat environment customized for rapid local testing.
- **Types:** Fully typed contract interactions using TypeChain.

## 🛠 Usage

### 1. Set up the Smart Contracts

Navigate to the `contracts` folder and run your local network:
```bash
cd contracts
npm install
npx hardhat node
```

In a new terminal window, deploy the example contracts to your local node:
```bash
npx hardhat run scripts/deploy.js --network localhost
```

### 2. Run the Next.js Frontend

```bash
cd frontend
npm install
npm run dev
```

Open `http://localhost:3000` to see your dApp! If you have MetaMask installed, you can connect your wallet and interact with the deployed test contract immediately.

## 📜 License

MIT License. Free to use for commercial projects. 

---
_If this boilerplate helped you launch your dApp faster, consider dropping a ⭐!_

