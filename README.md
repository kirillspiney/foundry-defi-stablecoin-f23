# Foundry DeFi Stablecoin (f23)

A decentralized stablecoin system built with Solidity and Foundry. The project implements a crypto-collateralized stablecoin pegged to USD, inspired by MakerDAO-like architectures.

## Overview

This project demonstrates a simplified DeFi protocol where users can deposit collateral (e.g., WETH, WBTC) and mint a USD-pegged stablecoin (DSC). It uses price oracles for collateral valuation and ensures overcollateralization for system stability.

### Key Features
- **Stability**: Maintains a 1 USD peg via collateral-backed issuance.
- **Collateralized**: Uses exogenous collateral (WETH/WBTC) instead of fiat assets.
- **Algorithmic Safety**: Users can only mint DSC with sufficient collateral; liquidation logic protects solvency.
- **Oracle Integration**: Fetches real-time asset prices from Chainlink or similar oracles.

## Project Structure

- `src/` — Solidity smart contracts (e.g., `DSCEngine.sol`, `DecentralizedStableCoin.sol`, `OracleLib.sol`).
- `test/` — Unit, fuzz, and invariant tests.
- `script/` — Deployment and interaction scripts.
- `lib/` — External dependencies (OpenZeppelin, Chainlink, etc.).
- `foundry.toml` — Foundry configuration.

## Getting Started

### Prerequisites
- [Foundry](https://book.getfoundry.sh/getting-started/installation)
- Node.js (optional for tooling)

### Installation

```bash
git clone https://github.com/kirillspiney/foundry-defi-stablecoin-f23.git
cd foundry-defi-stablecoin-f23
forge build
```

### Run Tests

```bash
forge test
```

### Run a Local Node (optional)

```bash
make anvil
```

Then deploy contracts locally or interact via scripts.

## Deployment

Set your environment variables:

```bash
export SEPOLIA_RPC_URL="https://..."
export PRIVATE_KEY="0x..."
```

Deploy on a test network:

```bash
make deploy ARGS="--network sepolia"
```

## Example Usage

```bash
# Deposit WETH and mint DSC
cast send <WETH_CONTRACT> "approve(address,uint256)" <DSC_ENGINE> 1ether --rpc-url $SEPOLIA_RPC_URL --private-key $PRIVATE_KEY
cast send <DSC_ENGINE> "depositCollateralAndMintDsc(address,uint256,uint256)" <WETH> 100000000000000000 50000000000000000 --rpc-url $SEPOLIA_RPC_URL --private-key $PRIVATE_KEY
```

## Architecture

- **DecentralizedStableCoin.sol** — ERC20 implementation of the DSC token.
- **DSCEngine.sol** — Core contract handling collateral deposits, minting, burning, and liquidations.
- **OracleLib.sol** — Library for price feed interactions and data freshness validation.

## Risks and Limitations

- Relies on external price feeds — oracle manipulation could impact safety.
- Requires overcollateralization — if collateral drops sharply, liquidations may fail.
- This project is **educational** and not intended for production without a formal audit.

## Developer Tools

Format code:

```bash
forge fmt
```

Check test coverage:

```bash
forge coverage
```

## License

MIT License

## Contributing

Pull requests are welcome! Ideas for improving stability mechanisms, adding governance, or expanding supported collaterals are appreciated.