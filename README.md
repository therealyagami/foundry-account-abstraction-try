# Foundry DAO F24

## Overview

This project implements **Account Abstraction (AA)** on Ethereum and zkSync, leveraging smart contracts to abstract the functionality typically reserved for Externally Owned Accounts (EOAs). The goal is to showcase how Account Abstraction can be used to simplify user interaction and transaction handling on Ethereum and zkSync, while reducing gas costs and enabling more flexibility in managing accounts.

### Key Objectives:

1. **Basic Account Abstraction on Ethereum**
   This section sets the foundation for Account Abstraction, but due to constraints like gas fees and complexity, it does not involve actual transaction sending on the Ethereum mainnet or testnet.

2. **Account Abstraction on zkSync**
   This project deploys an Account Abstraction contract on zkSync, utilizing zkSync's scalability and cost benefits. zkSync is a Layer 2 rollup solution built on Ethereum, using zero-knowledge proofs to enhance transaction throughput and minimize costs. The project will focus on AA transactions on zkSync.

3. **User Operation (UserOp) Transaction**
   The final objective is to send a User Operation (UserOp) transaction through the deployed Account Abstraction contract on zkSync, demonstrating how smart contract accounts manage and verify user transactions without the direct involvement of EOAs.

---

## Architecture

The project is composed of two main components:

### 1. **Minimal Account on Ethereum**
   This smart contract mimics an EOA’s ability to initiate and handle transactions. However, it does so through a smart contract account. It uses the `IEntryPoint` interface to facilitate communication between the contract and the Ethereum network. Key features of the contract include:
   - Signature validation using `ECDSA` and `MessageHashUtils`.
   - Execution of transactions with owner or entry point permission.
   - Validation of User Operations (UserOps).

### 2. **Minimal Account on zkSync**
   This contract replicates the Ethereum-based implementation but is adapted to work on zkSync. The zkSync version makes use of system contracts like the `NonceHolder` and follows a more complex lifecycle for transactions, as zkSync requires a multi-phase approach:
   - **Phase 1: Validation**
     The transaction is validated by ensuring nonce uniqueness and checking signatures.
   - **Phase 2: Execution**
     The validated transaction is passed to the sequencer, where it is executed, and in case of a paymaster transaction, post-transaction processes occur.

---

## Key Features

- **Account Abstraction (AA)**: Smart contract-based account management, removing the reliance on EOAs for initiating and managing transactions.
- **zkSync Support**: zkSync's Layer 2 technology enables faster, cheaper, and more efficient transactions.
- **Security Enhancements**: Ensures transactions are validated by the contract owner using signature verification techniques (`ECDSA`).
- **Gas Efficiency**: Optimized for minimizing gas costs, especially in the zkSync deployment.
- **Modular Design**: Reusable components for both Ethereum and zkSync that allow future extensibility.

---

## Tools & Technologies

- **Solidity**: The project is developed in Solidity, Ethereum's native smart contract programming language.
- **Foundry**: A powerful development framework for Ethereum smart contracts, used for testing, deploying, and managing the lifecycle of contracts.
- **OpenZeppelin**: Utilized for security features like signature verification and contract ownership.
- **zkSync**: A Layer 2 scaling solution, enabling fast and cheap transactions using zero-knowledge rollups.

---

## Deployment Instructions

### Prerequisites

Ensure you have the following installed on your local environment:

- Node.js
- Foundry (`forge`)
- zkSync network setup for Layer 2 transactions.

### Steps

1. Clone the repository:
```bash
   git clone https://github.com/therealyagami/foundry-dao-f24.git
```

Install dependencies:

```bash
forge install
Compile the smart contracts:
```

```bash
forge build
Deploy the smart contract on zkSync testnet:
```

```bash
forge create --rpc-url https://testnet.zksync.io --private-key YOUR_PRIVATE_KEY src/ZkMinimalAccount.sol:ZkMinimalAccount
```
## Sending a UserOp Transaction:
Once the contract is deployed, send a user operation through zkSync by interacting with the contract’s executeTransaction or validateTransaction functions. You may use the zkSync client or direct calls to trigger transactions.

### Roadmap & Future Improvements
**Extended Paymaster Support**: Explore zkSync’s paymaster contracts to facilitate sponsored transactions.

**Optimized Gas Usage**: Further optimize transaction execution to reduce gas usage in both Ethereum and zkSync implementations.

**Cross-Layer Compatibility**: Develop AA contracts that can seamlessly operate across multiple Layer 2 solutions, such as Arbitrum or Optimism, in addition to zkSync.

**Advanced UserOps**: Expand the range of supported user operations, including batch transactions, automated re-execution, and time-delayed execution.

### License
This project is licensed under the MIT License. See the LICENSE file for details.
