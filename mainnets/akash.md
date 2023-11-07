# Akash Network
|[AKASH SITE](https://akash.network/)|[AKASH DISCORD](https://discord.akash.network/)|[AKASH GITHUB](https://github.com/akash-network)|
|:--:|:--:|:--:|
|[AKASH TELEGRAM EN](https://t.me/AkashNW)|[AKASH TELEGRAM RU](https://t.me/akash_ru)|[AKASH TWITTER](https://twitter.com/akashnet_)|
|[GUIDE](https://github.com/DecloudNodesLab/Guides/blob/main/English/Deploy_CosmosSDK_node.md)|[SDL](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects/Akash_Network/akash_mainnet_deploy.yml)|[CLOUDMOS](https://deploy.cloudmos.io/)|
|[DELEGATE](https://restake.app/akash/akashvaloper1ax4c40gn3s74xxm75g6cmts3fw7rq64gq0kaj4a)|[EXPLORER](https://explorer.declab.pro/Akash)|[DECLOUD NODES LAB TELEGRAM CHANNEL](https://t.me/NodesLab)|



##### Endpoints

RPC: ```https://akash-sandbox.declab.pro/rpc```

API: ```https://akash-sandbox.declab.pro```

Peer:

##### Snapshot 

Link: ```https://akash-sandbox.declab.pro/latest.tar.lz4```

```
# Reset tendermint chain
akash tendermint unsafe-reset-all

# Download and unpack the archive
curl -o - -L https://akash-sandbox.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.akash
```

##### State sync

```
SNAP_RPC="https://akash-sandbox.declab.pro:443/rpc"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.akash/config/config.toml
```
