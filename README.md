# RWA-DeFi-Contract

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Solidity](https://img.shields.io/badge/Solidity-0.8.20-blue.svg)](https://soliditylang.org/)
[![Foundry](https://img.shields.io/badge/Built%20with-Foundry-FF6B6B.svg)](https://book.getfoundry.sh/)

> Real-World Asset (RWA) Tokenization Protocol for Real-Estate Auctions and Mortgage Lending

## 📋 Table of Contents
<a id="overview"></a>
- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Getting Started](#getting-started)
- [Development](#development)
- [Testing](#testing)
- [Security](#security)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

RWA-DeFi-Contract is a decentralized finance protocol that enables Real-World Asset tokenization, specifically designed for real estate auctions and mortgage lending. The protocol facilitates:

- **Global Lending**: Allows lenders worldwide to earn yields by supplying mortgage capital to residents of a city/jurisdiction
- **Mortgage Access**: Provides mortgage access to residents of jurisdictions (such as Prospera) who are blocked from traditional banking systems
- **On-Chain Real Estate**: Enables seamless real estate transactions with on-chain property ownership and mortgage management

<a id="features"></a>
## ✨ Features

### Core Capabilities

- **🏠 Property NFTs**: Legally compliant NFTs capable of representing real-world assets (RWAs). Property disputes can be resolved on-chain via arbitrator multisig
- **💰 Lending Pool**: Allows anyone to supply capital to the protocol and earn yields from mortgages. Includes tUSDC, an SEC-compliant interest-bearing token (unavailable to US Citizens)
- **📊 On-Chain Mortgages**: Gas-efficient amortization schedule implementation
- **🔨 Auctions**: Bidding mechanism enabling seamless real estate transactions. Users with active mortgages can accept bids, sell their property, pay off mortgage debt, and keep the difference—all in one transaction

### Interest Rate Models

The protocol supports multiple interest rate models:

- **Constant Rate**: Fixed/constant interest rate model
- **Two-Slope Model**: [Two-slope interest rate model](https://www.desmos.com/calculator/ryesiw7hau)
- **Smooth Curve Model**: [Smooth curve interest rate model](https://www.desmos.com/calculator/nimb8tbzgb)

<a id="architecture"></a>
## 🏗️ Architecture

### Protocol Structure

```
contracts/
├── protocol/
│   ├── state/
│   │   ├── State.sol          # Holds all protocol state variables
│   │   └── TargetManager.sol  # Handles upgrade and delegatecall logic
│   ├── proxy/
│   │   └── ProtocolProxy.sol  # Proxy mapping function selectors to implementations
│   └── logic/
│       ├── Auctions.sol        # Auction and bidding functionality
│       ├── Borrowing.sol       # Mortgage borrowing logic
│       ├── Info.sol            # External getters
│       ├── Initializer.sol     # Protocol initialization
│       ├── Residents.sol       # Resident verification and tracking
│       ├── interest/
│       │   ├── InterestConstant.sol
│       │   ├── Interest2Slopes.sol
│       │   └── InterestCurve.sol
│       └── loanStatus/
│           ├── Amortization.sol  # Gas-efficient amortization schedule
│           └── LoanStatus.sol    # Active mortgages vs defaults
├── pool/
│   └── Pool.sol                # Lending pool implementation
└── tokens/
    └── PropertyNft.sol         # Property NFT contract
```

### Key Design Patterns

- **Upgradeable Proxy Pattern**: Uses a proxy contract to enable upgrades while maintaining state
- **Storage Collision Prevention**: All logic contracts inherit from `State.sol` to avoid storage collisions
- **Modular Interest Models**: Pluggable interest rate models for flexible lending terms
- **Gas Optimization**: Efficient amortization calculations and state management

<a id="getting-started"></a>
## 🚀 Getting Started

### Prerequisites

- [Foundry](https://book.getfoundry.sh/getting-started/installation) (latest version)
- [Node.js](https://nodejs.org/) (v16 or higher)
- [Hardhat](https://hardhat.org/) (for deployment scripts)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/earthskyorg/RWA-DeFi-Contract.git
cd RWA-DeFi-Contract
```

2. Install dependencies:
```bash
# Install Foundry dependencies
forge install

# Install Node.js dependencies
npm install
```

3. Set up environment variables:
```bash
cp .env.example .env
# Edit .env with your configuration
```

### Compilation

```bash
# Using Foundry
forge build

# Using Hardhat
npx hardhat compile
```

<a id="development"></a>
## 💻 Development

### Project Structure

- `contracts/` - Solidity smart contracts
- `interfaces/` - Contract interfaces
- `test/` - Foundry test files
- `scripts/` - Deployment and utility scripts
- `financials/` - Python financial modeling scripts

### Code Quality

This project uses:
- **Foundry** for testing and deployment
- **Hardhat** for additional tooling
- **Solhint** for linting (configured)
- **Slither** for security analysis (recommended)

### Running Tests

```bash
# Run all tests
forge test

# Run with verbosity
forge test -vvv

# Run specific test file
forge test --match-path test/Invariant.t.sol

# Run with gas reporting
forge test --gas-report
```

<a id="testing"></a>
## 🧪 Testing

The test suite includes:

- **Unit Tests**: Individual contract functionality
- **Fuzz Tests**: Property-based testing (`Fuzz.t.sol`)
- **Invariant Tests**: System-wide invariants (`Invariant.t.sol`)
- **Handler Tests**: Stateful fuzzing handlers (`Handler.t.sol`)

### Test Coverage

```bash
forge coverage
```

<a id="security"></a>
## 🔒 Security

Security is a top priority. This project follows best practices:

- Comprehensive test coverage
- Formal verification considerations
- Regular security audits (recommended before mainnet deployment)
- Access control and role management
- Reentrancy protection

### Security Policy

See [SECURITY.md](SECURITY.md) for details on reporting security vulnerabilities.

### Audit Status

⚠️ **Warning**: This code has not been audited. Use at your own risk.

<a id="contributing"></a>
## 📝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Development Workflow

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

<a id="license"></a>
## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📞 Contact

- **Telegram**: [Tech Genie](https://t.me/opensea712)
- **Twitter**: [Tech Genie](https://x.com/shinytechapes)

## 🙏 Acknowledgments

- Built with [Foundry](https://book.getfoundry.sh/)
- Uses [OpenZeppelin](https://openzeppelin.com/) contracts
- [PRB Math](https://github.com/PaulRBerg/prb-math) for fixed-point arithmetic

---

**⚠️ Disclaimer**: This software is provided "as is" without warranty. Use at your own risk. Always conduct thorough security audits before deploying to mainnet.
