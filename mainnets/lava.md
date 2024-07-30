# Desmos

![](/assets/banner.png)

|[Site](https://lavanet.xyz/)|[Discord](https://discord.gg/Zb4e7g9tjE)|[Github](https://github.com/lavanet)|
|:--:|:--:|:--:|
|[Blog](https://www.lavanet.xyz/blog)|[Docs](https://docs.lavanet.xyz/)|[X](https://twitter.com/lavanetxyz)|
|[Guide](https://services.declab.pro/guides)|[Deploy file](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects/Lava/lava_mainnet_deploy.yml)|[Delegate to us](https://restake.app/lava/lava@valoper1ax4c40gn3s74xxm75g6cmts3fw7rq64gt8e7wl)|


[Lava EXPLORER](https://explorer.declab.pro/Lava)|
|:--:|

## Endpoints

|[**RPC**](https://lava.declab.pro:26613)|[**API**](https://lava.declab.pro)|
|:--:|:--:|

**Genesis:** ```https://lava.declab.pro/genesis.json```

```
wget -O ~/.lava/config/genesis.json https://lava.declab.pro/genesis.json --inet4-only
```

**Addrbook:** ```https://lava.declab.pro/addrbook.json```

```
wget -O ~/.lava/config/addrbook.json https://lava.declab.pro/addrbook.json --inet4-only
```

**Peer:** ```73ef1c0f9bc77fd925decf7fa41f22a35b5dc76d@lava.declab.pro:26615```

```
PEERS=73ef1c0f9bc77fd925decf7fa41f22a35b5dc76d@lava.declab.pro:26615
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.lava/config/config.toml
```

## Snapshot 

**Link:** ```https://lava.declab.pro/latest.tar.lz4```

```
# Reset tendermint chain
lava tendermint unsafe-reset-all

# Download and unpack the archive
curl -o - -L https://lava.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C ~/.lava
```

## State sync

```
RPC="https://lava.declab.pro:26613"

LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" ~/.lava/config/config.toml
```
