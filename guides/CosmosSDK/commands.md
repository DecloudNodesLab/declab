<p align="center"><img src="https://user-images.githubusercontent.com/23629420/219872517-2adc32b1-5f64-4d48-9a81-1e2ef6b01a53.png" </p>
  
<div align="center">  
  
|[Decloud Nodes Lab](https://declab.pro)|[Discord Decloud Nodes Lab](https://discord.gg/eDKdvjfUAS)|[Twitter Decloud Nodes Lab](https://twitter.com/NodesLab)|
|:--:|:--:|:--:|

</div>

# CLI templates for projects based on Cosmos SDK.
```
BINARY=PROJECT_BINARY_NAME # Set the binary file name of the project (example: akash - for Akash Network, gitopiad - for Gitopia).
DENOM=PROJECT_UTOKEN # Set the denom token (example: uakt - for Akash Network, ulore - for Gitopia).
CHAIN=PROJECT_CHAIN_ID # Set the chain-id project (example: akashnet-2 - for Akash Network, gitpoia - for Gitopia).
MONIKER=YOUR_MONIKER # Set your node name.
```
___

## Account (wallet) commands

Create wallet:

```
$BINARY keys add WALLET_NAME
```

Restore wallet:

```
$BINARY keys add WALLET_NAME --recover
```

Check balance:

```
$BINARY q bank balances ADDRESS
```

Send 1 token to another address:

```
$BINARY tx bank send \
SENDER_ADDRESS \
RECEIVER_ADDRESS \
1000000$DENOM \
---fees 1000$DENOM \
--chain-id $CHAIN
```

___

## Validator commands

Create a validator

```
$BINARY tx staking create-validator \
--amount 1000000$DENOM \
--pubkey=$($BINARY tendermint show-validator) \
--moniker $MONIKER \
--chain-id $CHAIN" \
--details YOUR_PUBLIC_SIGN \
--security-contact YOUR@EMAIL.COM \
--website www.example.com \
--commission-rate 0.10 \
--commission-max-rate 0.20 \
--commission-max-change-rate 0.01 \
--min-self-delegation="1000000" \
--gas="auto \
--from OWNER_ADDRESS \
--fees 1000$DENOM 
```

Check validator pubkey

```
$BINARY tendermint show-validator
```

Check validator

```
$BINARY query staking validator VALOPER_ADDRESS
```

```
$BINARY query staking validators --limit 1000000 -o json | jq '.validators[] | select(.description.moniker=="$MONIKER")' | jq
```
  
Collect commissions + rewards

```
$BINARY tx distribution withdraw-rewards VALOPER_ADDRESS --from OWNER_ADDRESS --fees 1000$DENOM --commission --chain-id $CHAIN -y
```

Delegate 1,000,000 'u' token to yourself

```
$BINARY tx staking delegate VALOPER_ADDRESS 1000000$DENOM --from OWNER_ADDRESS --fees 1000$DENOM --chain-id $CHAIN -y
```

___

## Voting commands
  
Proposals list

```
$BINARY q gov proposals
```
  
View the result of the vote

```
$BINARY q gov proposals --voter ADDRESS
```
  
Vote 'yes' for the proposal №1

```
$BINARY tx gov vote 1 yes --from ADDRESS --fees 1000$DENOM
```
  
Make a deposit to the offer

```
$BINARY tx gov deposit 1 1000000$DENOM --from ADDRESS --fees 1000$DENOM
```

Create an offer

```
$BINARY tx gov submit-proposal --title="Randomly reward" \
--description="Reward 10 testnet participants who completed more than 3 tasks" \
--type="Text" \
--deposit="11000000$DENOM" \
--from ADDRESS \
--fees 1000$DENOM 
```
___

## Network settings commands
  
Network settings

```
$BINARY q staking params
```

```
$BINARY q slashing params
```

Get out of jail

```
$BINARY tx slashing unjail --from OWNER_ADDRESS --fees 1000$DENOM -y
```

```
$BINARY q slashing signing-info $($BINARY tendermint show-validator)
```

Check Status

```
$BINARY status
```

___
