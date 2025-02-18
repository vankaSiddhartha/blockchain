# NFT Marketplace Technical Documentation

## Project Architecture

### Directory Structure

```
Blockchain/
└── nftmarketplace/
    └── src/
        ├── backend/
        │   ├── contracts/
        │   │   ├── Marketplace.sol
        │   │   └── NFT.sol
        │   └── test/
        │       └── MarketplaceTest.js
        └── frontend/
            ├── components/
            │   ├── Create.js
            │   ├── Home.js
            │   └── MyListedItems.js
            ├── componentsData/
            │   └── ContractABI/
            ├── utils/
            │   └── ipfs.js
            └── App.js
```

## Smart Contracts Architecture

### Marketplace.sol

The Marketplace contract inherits from ReentrancyGuard to prevent reentrancy attacks. This contract handles the core marketplace functionality including listing, buying, and managing NFTs.

Key Security Features:

- ReentrancyGuard: Prevents recursive calls during token transfers
- Pull Payment Pattern: Implements withdrawal pattern instead of direct transfers
- Access Control: Validates ownership and permissions for listings
- Input Validation: Thorough validation of price and token parameters
- Event Emission: Logs all critical state changes for transparency

### NFT.sol

Inherits from ERC721URIStorage for NFT functionality with metadata storage capabilities.

Security Measures:

- Access Control: Only authorized addresses can mint tokens
- URI Validation: Checks for valid metadata URIs
- Ownership Verification: Validates token ownership before operations
- Compliance: Follows ERC721 standard specifications

## Backend Implementation

### Smart Contract Testing

Located in `test/MarketplaceTest.js`, implements comprehensive testing scenarios:

- Listing creation and validation
- Purchase flow verification
- Access control testing
- Edge case handling
- Gas optimization verification

## Frontend Architecture

### React Components

#### Home.js (Marketplace)

- Implements marketplace interface
- Connects with smart contracts via ethers.js
- Handles MetaMask integration
- State management for marketplace items

#### Create.js (NFT Creation)

- IPFS integration for metadata storage
- Base64 encoding for image processing
- SHA256 hashing for content integrity
- MetaMask transaction handling

#### MyListedItems.js (DigiLocker)

- Personal NFT management interface
- Ownership verification
- Transaction history display

## Security Implementation

### Smart Contract Security

1. Reentrancy Protection:

```solidity
modifier nonReentrant() {
    require(!locked, "Reentrant call");
    locked = true;
    _;
    locked = false;
}
```

2. Access Control:

```solidity
modifier onlyOwner() {
    require(msg.sender == owner, "Not authorized");
    _;
}
```

### IPFS Implementation

Located in `utils/ipfs.js`:

- Content addressing using SHA256
- Base64 encoding for image data
- Decentralized storage integration
- Content integrity verification

## Algorithms Used

1. SHA256 Hashing:

   - Purpose: Content integrity verification
   - Implementation: Used for IPFS content addressing
   - Security: Cryptographic hash function for data integrity

2. Base64 Encoding:
   - Purpose: Image data conversion
   - Implementation: Converts binary image data to base64 strings
   - Usage: IPFS metadata storage

## Deployment Process

1. Local Development Setup:

```bash
cd nft_marketplace
npm install
```

2. Blockchain Initialization:

```bash
npx hardhat node
```

3. Smart Contract Deployment:

```bash
npx hardhat run src/backend/scripts/deploy.js --network localhost
```

## Security Considerations

1. Smart Contract Security:

   - Reentrancy protection
   - Access control implementation
   - Input validation
   - Event logging
   - Pull payment pattern

2. Frontend Security:

   - MetaMask integration security
   - Transaction signing validation
   - Input sanitization
   - Error handling

3. IPFS Security:
   - Content addressing verification
   - Hash validation
   - Metadata integrity checks

## Network Configuration

### MetaMask Setup:

1. Network Name: "Hardhat"
2. RPC URL: "http://127.0.0.1:8545"
3. Chain ID: 31337

## Best Practices Implemented

1. Smart Contract Development:

   - Gas optimization
   - Event logging
   - Modular design
   - Comprehensive testing

2. Frontend Development:

   - Component-based architecture
   - Clean code practices
   - Error handling
   - User experience considerations

3. Security Measures:
   - Authentication checks
   - Authorization validation
   - Data integrity verification
   - Secure storage implementation
