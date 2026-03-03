---
name: fuzz-invariant
description: Fuzz testing and invariant testing patterns for Foundry
metadata:
  tags: fuzz, invariant, stateless, stateful, handler, property-based
---

## Stateless Fuzz Testing

Any test function that accepts parameters becomes a fuzz test. Foundry generates random inputs automatically.

```solidity
function testFuzz_Deposit(uint256 amount) public {
    amount = bound(amount, 1, 100 ether);  // Constrain input range

    vm.deal(address(this), amount);
    vault.deposit{value: amount}();

    assertEq(vault.balanceOf(address(this)), amount);
}
```

Use `bound()` instead of `vm.assume()` when possible — `assume` discards inputs and can slow test runs.

## Invariant Testing

Invariant tests call random functions in random order to verify properties that must always hold.

### Basic Setup

```solidity
// test/invariants/VaultInvariant.t.sol
import {Test} from "forge-std/Test.sol";
import {Vault} from "../../src/Vault.sol";
import {VaultHandler} from "./VaultHandler.sol";

contract VaultInvariantTest is Test {
    Vault vault;
    VaultHandler handler;

    function setUp() public {
        vault = new Vault();
        handler = new VaultHandler(vault);

        // Tell Foundry to only call functions on the handler
        targetContract(address(handler));
    }

    function invariant_totalAssetsMatchBalance() public view {
        assertEq(
            vault.totalAssets(),
            address(vault).balance
        );
    }
}
```

### Handler Pattern

Handlers wrap contract interactions with valid preconditions and track state with ghost variables.

```solidity
// test/invariants/VaultHandler.sol
import {Test} from "forge-std/Test.sol";
import {Vault} from "../../src/Vault.sol";

contract VaultHandler is Test {
    Vault vault;

    // Ghost variables for tracking
    uint256 public ghost_totalDeposited;
    uint256 public ghost_totalWithdrawn;

    constructor(Vault _vault) {
        vault = _vault;
    }

    function deposit(uint256 amount) public {
        amount = bound(amount, 1, 10 ether);
        vm.deal(address(this), amount);
        vault.deposit{value: amount}();
        ghost_totalDeposited += amount;
    }

    function withdraw(uint256 amount) public {
        uint256 balance = vault.balanceOf(address(this));
        amount = bound(amount, 0, balance);
        if (amount == 0) return;
        vault.withdraw(amount);
        ghost_totalWithdrawn += amount;
    }
}
```

### Using Ghost Variables in Invariants

```solidity
function invariant_depositsMinusWithdrawals() public view {
    assertEq(
        address(vault).balance,
        handler.ghost_totalDeposited() - handler.ghost_totalWithdrawn()
    );
}
```

### Target Selectors

Restrict which functions the fuzzer calls:

```solidity
function setUp() public {
    // Only call these functions
    bytes4[] memory selectors = new bytes4[](2);
    selectors[0] = VaultHandler.deposit.selector;
    selectors[1] = VaultHandler.withdraw.selector;
    targetSelector(FuzzSelector(address(handler), selectors));
}
```

## Configuration

In `foundry.toml`:

```toml
[fuzz]
runs = 256            # Number of fuzz runs per test (default: 256)
max_test_rejects = 65536
seed = "0x1"          # Deterministic seed for reproducibility

[invariant]
runs = 256            # Number of invariant run sequences
depth = 15            # Calls per run sequence
fail_on_revert = false
```

Override per-test run count:

```bash
forge test --fuzz-runs 10000
```
