# Sentinelhub (Chain node)

![](/assets/banner.png)

|[Sentinel site](https://www.sentinel.co/)|[Sentinel Discord](https://discord.com/invite/mmAA8qF)|[Sentinel Github](https://github.com/sentinel-official)|
|:--:|:--:|:--:|
|[Sentinel Telegram](https://t.me/sentinel_co)|[Reddit](https://www.reddit.com/r/dVPN/u)|[Sentinel X](https://twitter.com/SentinelVPN)|
|[Guide](https://services.declab.pro/guides)|[Deploy file](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects/Sentinel-DVPN/sentinel_chain_deploy.yml)|[Delegate to us](https://restake.app/sentinel/sentvaloper1ax4c40gn3s74xxm75g6cmts3fw7rq64grgugsr)|


[Sentinel Network EXPLORER](https://explorer.declab.pro/Sentinel)|
|:--:|


## Endpoints

|[**RPC**](https://sentinel.declab.pro:26628)|[**API**](https://sentinel.declab.pro)|
|:--:|:--:|

**Genesis:** ```https://sentinel.declab.pro/genesis.json```

```
wget -O ~/.sentinelhub/config/genesis.json https://sentinel.declab.pro/genesis.json --inet4-only
```

**Addrbook:** ```https://sentinel.declab.pro/addrbook.json```

```
wget -O ~/.sentinelhub/config/addrbook.json https://sentinel.declab.pro/addrbook.json --inet4-only
```

**Peer:** ```73ef1c0f9bc77fd925decf7fa41f22a35b5dc76d@sentinel.declab.pro:26630```

```
PEERS=73ef1c0f9bc77fd925decf7fa41f22a35b5dc76d@sentinel.declab.pro:26630,0d9f4ae53eb69d4790e9633094b19e0ff18c6e82@5.10.24.84:26656,66d0d22dc5e1e542c200da1fc097dae5ea1f3b4e@195.201.175.156:17256,e323d088efd63c06f13922a452533a444f5cfb23@45.10.26.114:26656,d6d3b940785d0135e53e38bc4639e1cbce47e983@88.99.199.5:26656,5ace0e57784e34930360bf6cc00dd5265278f708@65.108.238.166:23956
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.sentinelhub/config/config.toml
```

## Snapshot 

**Link:** ```https://sentinel.declab.pro/latest.tar.lz4```

```
# Reset tendermint chain
sentinelhub tendermint unsafe-reset-all

# Download and unpack the archive
curl -o - -L https://sentinel.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C ~/.sentinelhub
```

## State sync

```
RPC="https://sentinel.declab.pro:26628"

LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" ~/.sentinelhub/config/config.toml
```
