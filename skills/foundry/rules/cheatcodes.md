---
name: cheatcodes
description: vm.* cheatcodes quick reference for Foundry testing
metadata:
  tags: cheatcodes, vm, prank, deal, warp, roll, expectRevert, expectEmit, mock
---

Cheatcodes are special functions on the `vm` object available in tests that inherit from `forge-std/Test.sol`.

## Identity & Caller

```solidity
vm.prank(address)              // Next call comes from address
vm.startPrank(address)         // All subsequent calls come from address
vm.stopPrank()                 // Stop pranking

vm.prank(sender, origin)       // Set both msg.sender and tx.origin
```

## Balances & Funding

```solidity
vm.deal(address, amount)       // Set ETH balance
hoax(address)                  // prank + deal 1 ether (convenience)
hoax(address, amount)          // prank + deal specific amount
deal(address(token), who, amount)  // Set ERC-20 balance (forge-std)
```

## Block & Time

```solidity
vm.warp(timestamp)             // Set block.timestamp
vm.roll(blockNumber)           // Set block.number
vm.fee(baseFee)                // Set block.basefee
vm.chainId(id)                 // Set block.chainid
skip(seconds)                  // Advance block.timestamp (forge-std)
rewind(seconds)                // Decrease block.timestamp (forge-std)
```

## Expectations

```solidity
// Expect the next call to revert
vm.expectRevert();
contract.failingFunction();

// Expect revert with specific message
vm.expectRevert("Insufficient balance");
contract.failingFunction();

// Expect revert with custom error
vm.expectRevert(abi.encodeWithSelector(CustomError.selector, arg1));
contract.failingFunction();

// Expect an event emission
vm.expectEmit(true, true, false, true);  // (topic1, topic2, topic3, data)
emit Transfer(from, to, amount);         // Expected event
contract.transfer(to, amount);           // Actual call
```

## Storage

```solidity
vm.store(address, slot, value)   // Write to storage slot
vm.load(address, slot)           // Read from storage slot
```

## Mocking

```solidity
// Mock a specific call
vm.mockCall(
    address(token),
    abi.encodeWithSelector(IERC20.balanceOf.selector, user),
    abi.encode(1000 ether)
);

// Clear mocks
vm.clearMockedCalls();
```

## Environment Variables

```solidity
vm.envUint("PRIVATE_KEY")       // Read uint from env
vm.envAddress("DEPLOYER")       // Read address from env
vm.envString("RPC_URL")         // Read string from env
vm.envBool("VERBOSE")           // Read bool from env
vm.envOr("KEY", defaultValue)   // Read with default
```

## Fuzzing Helpers

```solidity
// Bound a fuzz input to a range
amount = bound(amount, 1, 1000 ether);

// Assume a condition (skip input if false)
vm.assume(amount > 0);
```

## Snapshots

```solidity
uint256 id = vm.snapshot();    // Save EVM state
vm.revertTo(id);               // Restore EVM state
```

## Labels

```solidity
vm.label(address, "Treasury");  // Label address for trace readability
```
