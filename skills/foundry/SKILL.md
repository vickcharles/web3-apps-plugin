---
name: foundry
description: Foundry toolkit for Solidity smart contract development. Use when working with forge, cast, anvil, chisel, foundry.toml, vm.prank, vm.deal, vm.warp, vm.expectRevert, vm.expectEmit, vm.createFork, fuzz testing, invariant testing, forge build, forge test, forge create, forge script, Solidity compilation, smart contract deployment, Etherscan verification, gas reports, coverage, cheatcodes.
metadata:
  tags: foundry, forge, cast, anvil, chisel, solidity, smart-contracts, testing, deployment, cheatcodes, fuzz, invariant
---

# Foundry

Foundry is a fast Solidity development toolkit written in Rust. It is **pre-installed** in the sandbox — no installation needed.

**Components:**
- **Forge** — Build, test, and deploy Solidity contracts
- **Cast** — Interact with EVM chains from the CLI
- **Anvil** — Local Ethereum node for development
- **Chisel** — Solidity REPL for quick experimentation

## Quick Start

```bash
# Initialize a new project
forge init my-project
cd my-project

# Build contracts
forge build

# Run tests with verbosity
forge test -vv
```

## Project Layout

```
├── src/              # Solidity source contracts
├── test/             # Solidity test files (*.t.sol)
├── script/           # Deployment scripts (*.s.sol)
├── lib/              # Dependencies installed via forge install
├── out/              # Build artifacts (ABI, bytecode)
├── cache/            # Compiler cache
└── foundry.toml      # Project configuration
```

## Rules

Read individual rule files for detailed explanations and code examples:

- [rules/forge-build-test.md](rules/forge-build-test.md) - Build commands, test verbosity, filtering, gas reports, coverage
- [rules/forge-deploy.md](rules/forge-deploy.md) - Contract deployment with forge create and forge script
- [rules/cheatcodes.md](rules/cheatcodes.md) - vm.* cheatcodes quick reference for testing
- [rules/fuzz-invariant.md](rules/fuzz-invariant.md) - Fuzz testing and invariant testing patterns
- [rules/fork-testing.md](rules/fork-testing.md) - Fork testing against live networks
- [rules/cast.md](rules/cast.md) - Chain interaction with cast subcommands
- [rules/anvil.md](rules/anvil.md) - Local Ethereum node for development and testing
- [rules/chisel.md](rules/chisel.md) - Solidity REPL for quick experimentation
- [rules/foundry-toml.md](rules/foundry-toml.md) - foundry.toml configuration reference

## Sources

- https://book.getfoundry.sh (scraped: 2026-02-28)
- https://book.getfoundry.sh/reference/forge (scraped: 2026-02-28)
- https://book.getfoundry.sh/reference/cast (scraped: 2026-02-28)
- https://book.getfoundry.sh/cheatcodes (scraped: 2026-02-28)
