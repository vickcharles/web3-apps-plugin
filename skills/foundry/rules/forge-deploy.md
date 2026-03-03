---
name: forge-deploy
description: Contract deployment with forge create and forge script, Etherscan verification
metadata:
  tags: forge, deploy, create, script, broadcast, etherscan, verify
---

## Direct Deployment with forge create

```bash
# Deploy with private key
forge create src/Counter.sol:Counter \
  --rpc-url $RPC_URL \
  --private-key $PRIVATE_KEY

# Deploy with constructor args
forge create src/Token.sol:Token \
  --rpc-url $RPC_URL \
  --private-key $PRIVATE_KEY \
  --constructor-args "MyToken" "MTK" 18

# Deploy + verify on Etherscan
forge create src/Counter.sol:Counter \
  --rpc-url $RPC_URL \
  --private-key $PRIVATE_KEY \
  --verify \
  --etherscan-api-key $ETHERSCAN_API_KEY
```

## Scripted Deployment with forge script

Create a deploy script in `script/`:

```solidity
// script/Deploy.s.sol
import {Script} from "forge-std/Script.sol";
import {Counter} from "../src/Counter.sol";

contract DeployScript is Script {
    function run() external {
        uint256 deployerPrivateKey = vm.envUint("PRIVATE_KEY");

        vm.startBroadcast(deployerPrivateKey);

        Counter counter = new Counter();

        vm.stopBroadcast();
    }
}
```

```bash
# Dry run (simulation)
forge script script/Deploy.s.sol

# Broadcast to network
forge script script/Deploy.s.sol \
  --rpc-url $RPC_URL \
  --broadcast

# Broadcast + verify
forge script script/Deploy.s.sol \
  --rpc-url $RPC_URL \
  --broadcast \
  --verify \
  --etherscan-api-key $ETHERSCAN_API_KEY
```

## Verifying Existing Contracts

```bash
forge verify-contract <address> src/Counter.sol:Counter \
  --chain-id 1 \
  --etherscan-api-key $ETHERSCAN_API_KEY

# With constructor args
forge verify-contract <address> src/Token.sol:Token \
  --chain-id 1 \
  --etherscan-api-key $ETHERSCAN_API_KEY \
  --constructor-args $(cast abi-encode "constructor(string,string,uint8)" "MyToken" "MTK" 18)
```

## Environment Variable Pattern

Use `.env` files with `source .env` or `vm.envUint`/`vm.envAddress` in scripts:

```bash
# .env
PRIVATE_KEY=0xac0974...
RPC_URL=https://eth-mainnet.g.alchemy.com/v2/YOUR_KEY
ETHERSCAN_API_KEY=YOUR_KEY
```

**Never commit private keys.** Add `.env` to `.gitignore`.
