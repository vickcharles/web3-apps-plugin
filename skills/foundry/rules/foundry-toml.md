---
name: foundry-toml
description: foundry.toml configuration reference
metadata:
  tags: foundry.toml, config, compiler, optimizer, remappings, profiles
---

## Basic Configuration

```toml
[profile.default]
src = "src"
out = "out"
libs = ["lib"]
solc = "0.8.28"                    # Solidity compiler version
evm_version = "cancun"             # Target EVM version
optimizer = true
optimizer_runs = 200
via_ir = false                     # Use IR-based compilation
```

## Remappings

Map import paths to local directories:

```toml
remappings = [
    "@openzeppelin/contracts/=lib/openzeppelin-contracts/contracts/",
    "@uniswap/v3-core/=lib/v3-core/",
]
```

Or use a `remappings.txt` file (auto-detected):

```
@openzeppelin/contracts/=lib/openzeppelin-contracts/contracts/
```

## Fuzz Testing Config

```toml
[fuzz]
runs = 256                         # Fuzz iterations per test
max_test_rejects = 65536           # Max rejected inputs before failure
seed = "0x1"                       # Seed for reproducibility
```

## Invariant Testing Config

```toml
[invariant]
runs = 256                         # Number of sequences
depth = 15                         # Calls per sequence
fail_on_revert = false             # Whether reverts count as failures
```

## RPC Endpoints

Define named RPC endpoints for use with `--fork-url` and `vm.createFork`:

```toml
[rpc_endpoints]
mainnet = "${MAINNET_RPC_URL}"
optimism = "${OPTIMISM_RPC_URL}"
base = "${BASE_RPC_URL}"
sepolia = "${SEPOLIA_RPC_URL}"
localhost = "http://127.0.0.1:8545"
```

## Etherscan API Keys

For contract verification:

```toml
[etherscan]
mainnet = { key = "${ETHERSCAN_API_KEY}" }
optimism = { key = "${OPTIMISTIC_ETHERSCAN_API_KEY}", url = "https://api-optimistic.etherscan.io/api" }
base = { key = "${BASESCAN_API_KEY}", url = "https://api.basescan.org/api" }
```

## Filesystem Permissions

Control which paths Forge scripts can access:

```toml
[profile.default]
fs_permissions = [
    { access = "read", path = "./config" },
    { access = "read-write", path = "./output" },
]
```

## Profiles

Define different configurations per environment:

```toml
[profile.default]
optimizer = true
optimizer_runs = 200

[profile.ci]
optimizer = true
optimizer_runs = 10000
fuzz = { runs = 1000 }

[profile.lite]
optimizer = false
```

Activate with `FOUNDRY_PROFILE` environment variable:

```bash
FOUNDRY_PROFILE=ci forge test
```

## Gas Reports

```toml
[profile.default]
gas_reports = ["Counter", "Vault"]      # Only report gas for these contracts
gas_reports_ignore = ["Test*"]           # Ignore test contracts
```

## Formatter

```toml
[fmt]
line_length = 120
tab_width = 4
bracket_spacing = true
int_types = "long"                      # uint256 instead of uint
multiline_func_header = "params_first"
sort_imports = true
```

Format with:

```bash
forge fmt                   # Format all files
forge fmt --check           # Check formatting without modifying
```
