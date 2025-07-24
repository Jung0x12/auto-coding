# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Foundry-based Solidity smart contract development template with modern tooling. The project uses Node.js
packages (via Bun) for dependency management instead of git submodules, and includes comprehensive testing, linting, and
formatting tools.

## Development Commands

### Core Development

- `forge build` - Build contracts
- `forge test` - Run all tests
- `forge test -vvv` - Run tests with verbose output (shows console.log)
- `forge test --gas-report` - Run tests with gas usage report
- `forge coverage` - Generate test coverage report
- `forge fmt` - Format Solidity code

### Linting and Code Quality

- `bun run lint` - Run full lint check (Solidity + Prettier)
- `bun run lint:sol` - Lint only Solidity files (forge fmt + solhint)
- `bun solhint "{script,src,tests}/**/*.sol"` - Run Solhint directly
- `bun run prettier:check` - Check non-Solidity file formatting
- `bun run prettier:write` - Fix non-Solidity file formatting

### Testing Commands

- `forge test` - Basic test run
- `bun run test:coverage` - Same as `forge coverage`
- `bun run test:coverage:report` - Generate HTML coverage report (requires lcov)

### Deployment

- `forge script script/Deploy.s.sol --broadcast --fork-url http://localhost:8545` - Deploy to Anvil
- Requires `MNEMONIC` environment variable for non-test deployments

### Utilities

- `forge clean` - Clean build artifacts and cache
- `bun run clean` - Remove cache and out directories

## Project Structure

```
├── src/           # Smart contracts
├── tests/         # Test files (.t.sol)
├── script/        # Deployment scripts (.s.sol)
│   ├── Base.s.sol # Base script with broadcaster setup
│   └── Deploy.s.sol # Main deployment script
├── foundry.toml   # Foundry configuration
├── remappings.txt # Import remappings
└── package.json   # Node.js dependencies and scripts
```

## Key Configuration Files

- **foundry.toml**: Solidity 0.8.29, Shanghai EVM, optimizer enabled with 10k runs
- **remappings.txt**: Maps forge-std and OpenZeppelin imports to node_modules
- **.solhint.json**: Solidity linting rules (max complexity: 8, line length: 120)
- **package.json**: Contains all development scripts and dependencies

## Dependencies

- **forge-std**: Testing framework and utilities
- **@openzeppelin/contracts**: Standard contract library
- **solhint**: Solidity linter
- **prettier**: Code formatter for non-Solidity files

## Testing Patterns

The project includes examples of:

- Basic unit tests with assertions
- Fuzz testing with `vm.assume()` or `bound()`
- Fork testing against mainnet (requires `API_KEY_ALCHEMY`)
- Console logging with `console2.log()` (visible with `-vvv` flag)

## Script Architecture

- **BaseScript**: Abstract base with broadcaster setup logic
- **Deploy**: Concrete deployment script extending BaseScript
- Uses `broadcast()` modifier for transaction broadcasting
- Supports both `ETH_FROM` and `MNEMONIC` environment variables
