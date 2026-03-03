---
name: fork-testing
description: Fork testing against live networks with Foundry
metadata:
  tags: fork, mainnet, rpc, createFork, selectFork, impersonate
---

## CLI Fork Testing

Run tests against a forked network directly from the command line:

```bash
# Fork mainnet
forge test --fork-url https://eth-mainnet.g.alchemy.com/v2/YOUR_KEY

# Fork at a specific block (deterministic)
forge test --fork-url $RPC_URL --fork-block-number 18000000
```

## In-Test Fork Management

Use `vm.createFork` for granular control within tests:

```solidity
contract ForkTest is Test {
    uint256 mainnetFork;
    uint256 optimismFork;

    function setUp() public {
        // Create forks (does not activate them)
        mainnetFork = vm.createFork(vm.envString("MAINNET_RPC_URL"));
        optimismFork = vm.createFork(vm.envString("OPTIMISM_RPC_URL"));
    }

    function test_MainnetState() public {
        vm.selectFork(mainnetFork);
        assertEq(vm.activeFork(), mainnetFork);

        // Now all calls use mainnet state
        uint256 balance = IERC20(DAI).balanceOf(whale);
        assertGt(balance, 0);
    }

    function test_CrossFork() public {
        vm.selectFork(mainnetFork);
        uint256 mainnetBalance = address(whale).balance;

        vm.selectFork(optimismFork);
        uint256 optimismBalance = address(whale).balance;

        // Balances differ across forks
    }
}
```

## Pinning to a Block

Pin forks to a specific block for deterministic tests:

```solidity
mainnetFork = vm.createFork(rpcUrl, 18000000);
```

## Impersonating Accounts

Combine forking with `vm.prank` to act as any on-chain address:

```solidity
function test_SwapAsWhale() public {
    vm.selectFork(mainnetFork);

    address whale = 0xAb5801a7D398351b8bE11C439e05C5B3259aeC9B;

    vm.prank(whale);
    IERC20(DAI).transfer(address(this), 1000 ether);
}
```

## RPC Endpoint Aliases

Define aliases in `foundry.toml` to avoid hardcoding URLs:

```toml
[rpc_endpoints]
mainnet = "${MAINNET_RPC_URL}"
optimism = "${OPTIMISM_RPC_URL}"
base = "${BASE_RPC_URL}"
sepolia = "${SEPOLIA_RPC_URL}"
```

Then use aliases:

```solidity
mainnetFork = vm.createFork("mainnet");
```

Or from the CLI:

```bash
forge test --fork-url mainnet
```

## Caching

Foundry caches forked state locally in `~/.foundry/cache/rpc/`. Clear with:

```bash
forge clean
```

Disable caching:

```toml
[profile.default]
no_storage_caching = true
```
