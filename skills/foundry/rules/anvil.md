---
name: anvil
description: Local Ethereum node for development and testing
metadata:
  tags: anvil, local, node, fork, accounts, mining, rpc
---

## Starting Anvil

```bash
anvil                          # Start with defaults (port 8545)
anvil --port 8546              # Custom port
anvil --accounts 20            # Number of pre-funded accounts (default: 10)
anvil --balance 10000          # Initial ETH balance per account (default: 10000)
anvil --block-time 12          # Auto-mine every 12 seconds
anvil --chain-id 31337         # Custom chain ID (default: 31337)
```

## Fork Mode

Fork a live network for local development:

```bash
anvil --fork-url https://eth-mainnet.g.alchemy.com/v2/YOUR_KEY
anvil --fork-url $RPC_URL --fork-block-number 18000000
```

All state from the forked chain is available locally. New transactions are mined locally.

## Pre-funded Accounts

Anvil provides 10 pre-funded accounts by default, each with 10,000 ETH. The first account:

```
Address: 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266
Key:     0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80
```

**Never use these keys on a real network.**

## Mining Modes

```bash
anvil                          # Auto-mine (mine on every transaction)
anvil --no-mining              # Manual mining only
anvil --block-time 5           # Interval mining (every 5 seconds)
```

Manual mining via RPC:

```bash
cast rpc evm_mine --rpc-url http://localhost:8545
```

## Impersonation

Send transactions as any address without its private key:

```bash
# Impersonate an address
cast rpc anvil_impersonateAccount <address> --rpc-url http://localhost:8545

# Send as that address
cast send <to> --value 1ether --from <impersonated> --rpc-url http://localhost:8545 --unlocked

# Stop impersonating
cast rpc anvil_stopImpersonatingAccount <address> --rpc-url http://localhost:8545
```

## Special JSON-RPC Methods

```bash
# Advance time
cast rpc evm_increaseTime 3600 --rpc-url http://localhost:8545

# Set next block timestamp
cast rpc evm_setNextBlockTimestamp 1700000000 --rpc-url http://localhost:8545

# Mine a block
cast rpc evm_mine --rpc-url http://localhost:8545

# Snapshot and revert
cast rpc evm_snapshot --rpc-url http://localhost:8545      # Returns snapshot ID
cast rpc evm_revert <id> --rpc-url http://localhost:8545   # Revert to snapshot

# Set balance
cast rpc anvil_setBalance <address> 0xDE0B6B3A7640000 --rpc-url http://localhost:8545

# Set storage
cast rpc anvil_setStorageAt <address> <slot> <value> --rpc-url http://localhost:8545

# Reset fork
cast rpc anvil_reset --params '[{"forking":{"jsonRpcUrl":"'$RPC_URL'"}}]' --rpc-url http://localhost:8545
```

## State Persistence

Dump and load Anvil state for reproducible environments:

```bash
anvil --dump-state state.json              # Dump state on exit
anvil --load-state state.json              # Load state on start
```
