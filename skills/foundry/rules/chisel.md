---
name: chisel
description: Solidity REPL for quick experimentation
metadata:
  tags: chisel, repl, solidity, interactive, experiment
---

## Starting Chisel

```bash
chisel                         # Start REPL
chisel --fork-url $RPC_URL     # Start with forked state
```

## Basic Usage

Type Solidity expressions directly:

```
~ uint256 x = 42;
~ x + 8
Type: uint256
|- Value: 50

~ address(0xdead).balance
Type: uint256
|- Value: 0

~ type(uint256).max
Type: uint256
|- Value: 115792089237316195423570985008687907853269984665640564039457584007913129639935
```

## Multi-line Functions

Define and call functions interactively:

```
~ function double(uint256 n) pure returns (uint256) {
~     return n * 2;
~ }
~ double(21)
Type: uint256
|- Value: 42
```

## Slash Commands

```
!help          Show available commands
!source        Show all Solidity source generated in the session
!clear         Clear all session code
!fork <url>    Fork a network in the current session
!reset         Reset the session
!quit          Exit Chisel
```

## Fork Mode

Access live chain state in the REPL:

```bash
chisel --fork-url https://eth-mainnet.g.alchemy.com/v2/YOUR_KEY
```

```
~ IERC20(0x6B175474E89094C44Da98b954EedeAC495271d0F).name()
Type: string
|- Value: "Dai Stablecoin"
```

## Use Cases

- Quickly test ABI encoding/decoding
- Verify Solidity math and type behavior
- Query on-chain state interactively
- Prototype contract logic before writing tests
