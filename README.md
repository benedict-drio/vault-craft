# VaultCraft Protocol

> Revolutionary community-driven treasury management protocol that democratizes investment decisions through tokenized participation and collective governance.

## Overview

VaultCraft transforms traditional fund management by creating a transparent, decentralized ecosystem where stakeholders directly control capital allocation. Through innovative time-locked staking mechanisms and weighted governance voting, participants earn representation tokens that grant proportional decision-making power over treasury operations.

The protocol features sophisticated proposal lifecycle management, automated execution systems, and built-in security measures including minimum thresholds, duration controls, and anti-manipulation safeguards. Perfect for DAOs, investment clubs, and communities seeking democratic financial governance without traditional intermediaries.

## Key Features

- **Time-locked Staking**: Secure STX deposits with configurable lock periods
- **Weighted Voting**: Governance power proportional to stake commitment
- **Automated Execution**: Consensus-driven proposal implementation
- **Multi-layered Security**: Comprehensive error handling and validation
- **Gas Optimization**: Cost-effective governance operations

## System Architecture

### Core Components

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Staking       │    │   Governance    │    │   Treasury      │
│   Module        │    │   Module        │    │   Module        │
├─────────────────┤    ├─────────────────┤    ├─────────────────┤
│ • Deposits      │    │ • Proposals     │    │ • Fund Transfer │
│ • Withdrawals   │    │ • Voting        │    │ • Execution     │
│ • Token Minting │    │ • Power Calc    │    │ • Security      │
│ • Time Locks    │    │ • Validation    │    │ • Verification  │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                        │                        │
         └────────────────────────┼────────────────────────┘
                                  │
                    ┌─────────────────┐
                    │   Protocol      │
                    │   State         │
                    ├─────────────────┤
                    │ • Balances      │
                    │ • Deposits      │
                    │ • Proposals     │
                    │ • Votes         │
                    └─────────────────┘
```

### Contract Architecture

The VaultCraft protocol is implemented as a single Clarity smart contract with modular functions:

#### State Management

- **Balances Map**: Tracks governance token holdings
- **Deposits Map**: Stores staking information with time locks
- **Proposals Map**: Manages governance proposal lifecycle
- **Votes Map**: Records voting decisions and prevents double voting

#### Function Categories

1. **Initialization**: Protocol setup and configuration
2. **Staking Operations**: Deposit/withdrawal with token mechanics
3. **Governance**: Proposal creation, voting, and execution
4. **Query Functions**: Read-only data access

## Data Flow

### 1. Staking Flow

```
User STX → Protocol Vault → Governance Tokens → Voting Power
    ↓
Time Lock Applied → Withdrawal Restriction → Security Enforcement
```

### 2. Governance Flow

```
Proposal Creation → Validation → Voting Period → Execution
       ↓              ↓            ↓            ↓
   Token Holder   Input Check   Weight Calc   Fund Transfer
```

### 3. Execution Flow

```
Proposal Approved → Consensus Check → Fund Transfer → State Update
       ↓                ↓               ↓            ↓
   Vote Tally      Majority Rule    STX Movement   Executed Flag
```

## Getting Started

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) for development and testing
- [Stacks CLI](https://docs.stacks.co/docs/command-line-interface) for deployment
- Node.js and npm for testing framework

### Installation

1. Clone the repository:

```bash
git clone https://github.com/benedict-drio/vault-craft.git
cd vault-craft
```

2. Install dependencies:

```bash
npm install
```

3. Check contract syntax:

```bash
clarinet check
```

4. Run tests:

```bash
npm test
```

### Contract Deployment

1. Initialize the protocol (owner only):

```clarity
(contract-call? .vault-craft initialize)
```

2. Set minimum deposit threshold (default: 1 STX):

```clarity
;; Configured via minimum-deposit variable
```

## Protocol Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| Minimum Duration | 144 blocks | ~1 day minimum proposal duration |
| Maximum Duration | 20,160 blocks | ~14 days maximum proposal duration |
| Minimum Deposit | 1,000,000 µSTX | 1 STX minimum stake requirement |
| Lock Period | 1,440 blocks | ~10 days withdrawal restriction |

## Core Functions

### Staking Operations

#### `deposit(amount: uint)`

Stakes STX tokens and receives governance tokens in return.

- Validates minimum deposit threshold
- Applies time lock for withdrawal security
- Mints proportional governance tokens

#### `withdraw(amount: uint)`

Withdraws staked STX after lock period expires.

- Checks time lock expiration
- Burns governance tokens
- Returns STX to user

### Governance Operations

#### `create-proposal(description, amount, target, duration)`

Creates new governance proposal for fund allocation.

- Validates input parameters
- Requires token holder status
- Sets expiration based on duration

#### `vote(proposal-id, vote-for)`

Casts weighted vote on active proposal.

- Prevents double voting
- Calculates voting power from token balance
- Updates proposal vote tallies

#### `execute-proposal(proposal-id)`

Executes approved proposal after expiration.

- Validates majority approval
- Transfers funds to target address
- Marks proposal as executed

### Query Functions

#### `get-balance(account)`

Returns governance token balance for account.

#### `get-proposal(proposal-id)`

Retrieves proposal details and current status.

#### `get-deposit-info(account)`

Returns staking information including lock status.

## Security Features

### Input Validation

- Comprehensive parameter checking
- Range validation for durations
- Target address verification

### Access Control

- Owner-only initialization
- Token holder governance rights
- Time-locked withdrawals

### Anti-Manipulation

- Double voting prevention
- Minimum stake requirements
- Proposal expiration enforcement

## Error Codes

| Code | Description |
|------|-------------|
| 100 | Owner only operation |
| 101 | Protocol not initialized |
| 102 | Already initialized |
| 103 | Insufficient balance |
| 104 | Invalid amount |
| 105 | Unauthorized operation |
| 106 | Proposal not found |
| 107 | Proposal expired |
| 108 | Already voted |
| 109 | Below minimum threshold |
| 110 | Tokens still locked |

## Testing

The protocol includes comprehensive test coverage:

```bash
# Run all tests
npm test

# Check contract syntax
clarinet check

# Run specific test file
npx vitest tests/vault-craft.test.ts
```

## Use Cases

### DAO Treasury Management

- Democratic fund allocation decisions
- Transparent proposal process
- Stakeholder-driven governance

### Investment Clubs

- Collective investment decisions
- Risk distribution through voting
- Member commitment through staking

### Community Funds

- Grant distribution mechanisms
- Community-driven development funding
- Transparent resource allocation

## Contributing

1. Fork the repository
2. Create feature branch: `git checkout -b feature/new-feature`
3. Commit changes: `git commit -am 'Add new feature'`
4. Push to branch: `git push origin feature/new-feature`
5. Submit pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For questions, issues, or contributions:

- Open an issue on GitHub
- Join our community discussions
- Review the documentation
