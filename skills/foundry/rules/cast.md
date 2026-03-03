---
name: cast
description: Chain interaction with cast subcommands
metadata:
  tags: cast, call, send, balance, abi, encode, decode, tx
---

## Reading from Contracts

```bash
# Call a view function
cast call <contract> "balanceOf(address)(uint256)" <address> --rpc-url $RPC_URL

# Call with named output
cast call <contract> "name()(string)" --rpc-url $RPC_URL

# Call with multiple return values
cast call <contract> "getReserves()(uint112,uint112,uint32)" --rpc-url $RPC_URL
```

## Writing to Contracts

```bash
# Send a transaction
cast send <contract> "transfer(address,uint256)" <to> <amount> \
  --rpc-url $RPC_URL \
  --private-key $PRIVATE_KEY

# Send ETH
cast send <to> --value 1ether \
  --rpc-url $RPC_URL \
  --private-key $PRIVATE_KEY
```

## Balance & Block Queries

```bash
cast balance <address> --rpc-url $RPC_URL           # ETH balance (wei)
cast balance <address> --rpc-url $RPC_URL --ether    # ETH balance (ether)
cast block latest --rpc-url $RPC_URL                  # Latest block info
cast block-number --rpc-url $RPC_URL                  # Latest block number
cast chain-id --rpc-url $RPC_URL                      # Chain ID
cast gas-price --rpc-url $RPC_URL                     # Current gas price
```

## ABI Encode & Decode

```bash
# Encode function calldata
cast calldata "transfer(address,uint256)" 0x1234... 1000000

# ABI-encode constructor args
cast abi-encode "constructor(string,string,uint8)" "MyToken" "MTK" 18

# Decode calldata
cast 4byte-decode 0xa9059cbb000000...

# Decode ABI-encoded output
cast abi-decode "balanceOf(address)(uint256)" 0x000000...
```

## Unit Conversions

```bash
cast to-wei 1.5 ether          # 1500000000000000000
cast from-wei 1500000000000000000   # 1.500000000000000000
cast to-hex 255                 # 0xff
cast to-dec 0xff                # 255
cast to-base 255 hex            # 0xff
```

## Transaction Inspection

```bash
cast tx <tx-hash> --rpc-url $RPC_URL           # Transaction details
cast receipt <tx-hash> --rpc-url $RPC_URL       # Transaction receipt
cast receipt <tx-hash> logs --rpc-url $RPC_URL  # Transaction logs
```

## ENS

```bash
cast resolve-name vitalik.eth --rpc-url $RPC_URL    # ENS -> address
cast lookup-address <address> --rpc-url $RPC_URL     # Address -> ENS
```

## Utility

```bash
cast sig "transfer(address,uint256)"    # Function selector: 0xa9059cbb
cast keccak "Hello"                     # Keccak-256 hash
cast wallet new                         # Generate new keypair
cast wallet address --private-key $KEY  # Derive address from key
```
