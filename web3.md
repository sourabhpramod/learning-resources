# Getting started on a web3 project with hardhat:

```Bash
nvm use 18

```
```Bash
yarn add --dev hardhat
```
```Bash
yarn hardhat

```
```
yarn add --dev @nomiclabs/hardhat-ethers@npm:hardhat-deploy-ethers ethers @nomiclabs/hardhat-etherscan @nomiclabs/hardhat-waffle chai ethereum-waffle hardhat hardhat-contract-sizer hardhat-deploy hardhat-gas-reporter prettier prettier-plugin-solidity solhint solidity-coverage dotenv
```

### In hardhat.config.js file

```javascript

require("@nomiclabs/hardhat-waffle")
require("@nomiclabs/hardhat-etherscan")
require("hardhat-deploy")
require("solidity-coverage")
require("hardhat-gas-reporter")
require("hardhat-contract-sizer")
require("dotenv").config()

/**
 * @type import('hardhat/config').HardhatUserConfig
 */
```

### To compile:
```
yarn hardhat compile
```

## Tools
### Web3 Tools & Services

- **Chainlink Oracles**:  
  - Fetch off-chain data and deliver it to smart contracts.
  - Connect smart contracts to external data sources (e.g., prices, weather).

- **Chainlink Keepers**:  
  - Automate smart contract functions.
  - Monitor conditions and trigger actions without manual intervention.

- **The Graph**:  
  - Indexes blockchain data for easy querying.
  - Allows dApps to efficiently retrieve on-chain data.

- **IPFS (InterPlanetary File System)**:  
  - Decentralized storage for hosting and sharing files.
  - Enables permanent, distributed file storage for dApps.

- **Arweave**:  
  - Permanent decentralized storage network.
  - Used for long-term data storage on the blockchain.

- **ENS (Ethereum Name Service)**:  
  - Provides human-readable domain names for Ethereum addresses.
  - Simplifies sending transactions by replacing long addresses with easy-to-read names.

- **Infura**:  
  - Provides APIs and tools to connect dApps to Ethereum and IPFS.
  - Allows developers to interact with blockchain networks without running their own nodes.

- **Alchemy**:  
  - Blockchain infrastructure platform for developers.
  - Offers tools to monitor, build, and scale dApps across various chains.

- **Pocket Network**:  
  - Decentralized API service for blockchain data.
  - Provides access to blockchain networks without central points of failure.

- **Moralis**:  
  - Web3 backend platform.
  - Offers APIs for fast development of dApps, handling authentication, and interaction with smart contracts.

- **Optimism**:  
  - Layer 2 scaling solution for Ethereum.
  - Increases transaction throughput and reduces gas fees using optimistic rollups.

- **Arbitrum**:  
  - Layer 2 scaling solution using optimistic rollups.
  - Enables faster, cheaper transactions while leveraging Ethereum’s security.

- **ZK-Rollups**:  
  - Layer 2 scaling solution that bundles multiple transactions into one.
  - Uses zero-knowledge proofs for efficient validation.

- **Polygon**:  
  - Layer 2 scaling platform for Ethereum.
  - Provides a scalable and low-cost solution for dApps while maintaining compatibility with Ethereum.

- **Ceramic Network**:  
  - Decentralized platform for building Web3 applications.
  - Offers a dynamic data layer for managing user-generated content across dApps.

- **Lit Protocol**:  
  - Decentralized access control for Web3 apps.
  - Enables encryption, access control, and sharing of content across decentralized networks.

These tools help developers build decentralized applications (dApps) with better data access, automation, scalability, and user experience.
