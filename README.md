<div classname="logo">

<p align="center">
  <img height="300" height="auto" src="https://user-images.githubusercontent.com/78480857/208048940-257c3d9c-3dae-4f6d-ad0d-bba3f4ceb541.png">
</div>


# PLANQ MAINNET

- [Website](https://planq.network/)

- [Explorer](https://explorer.planq.network/)

- [Discord](https://discord.gg/zmjTn49k)

- [Reddit](https://www.reddit.com/r/planq_network)

- [Whitepaper](https://planq.network/whitepaper)

- [Twitter](https://twitter.com/PlanqFoundation)

## Hardware requirements
- OS : Ubuntu Linux 20.04 (LTS) x64

- Read Access Memory : 8 GB (higher better)

- CPU : 4 core (higher better)

- Disk: 250 GB SSD Storage (higher better)

- Bandwidth: 1 Gbps for Download / 100 Mbps for Upload


## Automatic Instalation:
```
wget -O planq.sh https://raw.githubusercontent.com/DiscoverMyself/Planq-Mainnet/main/planqscript && chmod +x planq.sh && ./planq.sh
```

## Manual Instalation
Planq [Official Docs](https://docs.planq.network/)


## Wallet Configuration
**Add new wallet**
```
planqd keys add $WALLET
```

**Recover wallet**
```
planqd keys add $WALLET --recover
```

**Wallet list**
```
planqd keys list
```

**Check Balance**
```
planqd query bank balances $(planqd keys show wallet -a)
```

**Delete Wallet**
```
planqd keys delete $WALLET
```


## Validator Configuration
**Create Validator**
```
planqd tx staking create-validator \
  --amount=1000000atplanq \
  --pubkey=$(planqd tendermint show-validator) \
  --moniker="$NODENAME \
  --chain-id=$PLANQ_CHAIN_ID \
  --commission-rate="0.05" \
  --commission-max-rate="0.10" \
  --commission-max-change-rate="0.01" \
  --min-self-delegation="1000000" \
  --gas="auto" \
  --gas-prices="0.025atplanq" \
  --from=$WALLET
```

**Check Validator address**

```
planqd keys show wallet --bech val -a
```

**Edit Validator**

```
planqd tx staking edit-validator \
  --moniker=$NODENAME \
  --identity=<your_keybase_id> \
  --website="<your_website>" \
  --details="<your_validator_description>" \
  --chain-id=$PLANQ_CHAIN_ID \
  --from=$WALLET
```
 
**Delegate to Validator**
```
planqd tx staking delegate $(planqd tendermint show-validator) 1000000atplanq --from $WALLET --chain-id $PLANQ_CHAIN_ID --fees 5000atplanq
```

**Unjail Validator**
```
planqd tx slashing unjail \
  --broadcast-mode=block \
  --from=$WALLET \
  --chain-id=$PLANQ_CHAIN_ID \
  --gas=auto --gas-adjustment 1.4
```
  
**Useful Commands**
1. Synchronization info

`
planqd status 2>&1 | jq .SyncInfo
`

2. Validator Info

`
planqd status 2>&1 | jq .ValidatorInfo
`

3. Node Info

`
planqd status 2>&1 | jq .NodeInfo
`

4. Show Node ID

`
planqd tendermint show-node-id
`

5. Delete Node

```
systemctl stop planqd
systemctl disable planqd
rm -rvf .planqd
rm -rvf planq.sh
rm -rvf planq
```

