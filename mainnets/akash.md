# Akash Network

|[Akash site](https://akash.network/)|[Akash Discord](https://discord.akash.network/)|[Akash Github](https://github.com/akash-network)|
|:--:|:--:|:--:|
|[Akash Telegram EN](https://t.me/AkashNW)|[Akash Telegram RU](https://t.me/akash_ru)|[Akash X](https://twitter.com/akashnet_)|
|[Guide](https://github.com/DecloudNodesLab/Guides/blob/main/English/Deploy_CosmosSDK_node.md)|[Delegate to us](https://restake.app/akash/akashvaloper1ax4c40gn3s74xxm75g6cmts3fw7rq64gq0kaj4a)|[EXPLORER](https://explorer.declab.pro/Akash)|


##### Endpoints

RPC: ```https://akash.declab.pro/rpc```

API: ```https://akash.declab.pro```

Peer:

##### Snapshot 

Link: ```https://akash.declab.pro/latest.tar.lz4```

```
# Reset tendermint chain
akash tendermint unsafe-reset-all

# Download and unpack the archive
curl -o - -L https://akash.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.akash
```

##### State sync

```
SNAP_RPC="https://akash.declab.pro:443/rpc"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.akash/config/config.toml
```
