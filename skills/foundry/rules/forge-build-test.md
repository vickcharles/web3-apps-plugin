---
name: forge-build-test
description: Build commands, test verbosity levels, filtering, gas reports, and coverage
metadata:
  tags: forge, build, test, gas, coverage, compilation
---

## Building

```bash
forge build                    # Compile all contracts
forge build --sizes            # Show contract sizes
forge build --force            # Force recompile (ignore cache)
```

## Running Tests

Test files live in `test/` and must end with `.t.sol`. Test functions must be prefixed with `test`.

```solidity
// test/Counter.t.sol
import {Test} from "forge-std/Test.sol";
import {Counter} from "../src/Counter.sol";

contract CounterTest is Test {
    Counter counter;

    function setUp() public {
        counter = new Counter();
    }

    function test_Increment() public {
        counter.increment();
        assertEq(counter.number(), 1);
    }

    function testFail_Decrement() public {
        // testFail_ prefix expects a revert
        counter.decrement(); // reverts if number is 0
    }
}
```

## Verbosity Levels

```bash
forge test              # No logs
forge test -v           # Logs from failing tests
forge test -vv          # Logs + emit logs from all tests
forge test -vvv         # Stack traces for failing tests
forge test -vvvv        # Stack traces + setup traces
forge test -vvvvv       # All traces
```

## Filtering Tests

```bash
forge test --match-test "test_Increment"       # Match test function name
forge test --match-contract "CounterTest"       # Match contract name
forge test --match-path "test/Counter.t.sol"    # Match file path
forge test --no-match-test "testFuzz_"          # Exclude tests
```

## Gas Reports

```bash
forge test --gas-report                # Gas usage per function
forge snapshot                         # Save gas snapshot to .gas-snapshot
forge snapshot --diff                  # Compare against saved snapshot
```

## Coverage

```bash
forge coverage                         # Coverage summary
forge coverage --report lcov           # Generate lcov report
```

## Assertions (forge-std)

```solidity
assertEq(a, b);                    // Equality
assertApproxEqAbs(a, b, delta);    // Approximate equality (absolute)
assertApproxEqRel(a, b, pct);      // Approximate equality (relative, 1e18 = 100%)
assertGt(a, b);                    // Greater than
assertLt(a, b);                    // Less than
assertTrue(condition);              // Boolean true
```
