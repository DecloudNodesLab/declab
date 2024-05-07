# Desmos

![](/assets/banner.png)

|[Site](https://desmos.network/)|[Discord](https://discord.desmos.network/)|[Github](https://github.com/desmos-labs/desmos)|
|:--:|:--:|:--:|
|[Medium](https://medium.com/desmosnetwork)|[Instagram](https://instagram.com/desmosnetwork)|[X](https://twitter.com/desmosnetwork)|
|[Guide](https://services.declab.pro/guides)|[Deploy file](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects/Desmos/desmos_mainnet.yml)|[Delegate to us](https://restake.app/desmos/desmosvaloper1fkpnxtn4nvm27zkpyuvcz3rpa9rzxm70q4v8sn)|


[Desmos EXPLORER](https://explorer.declab.pro/Desmos)|
|:--:|

## Endpoints

|[**RPC**](https://desmos.declab.pro:26613)|[**API**](https://desmos.declab.pro)|
|:--:|:--:|

**Genesis:** ```https://desmos.declab.pro/genesis.json```

```
wget -O ~/.desmos/config/genesis.json https://desmos.declab.pro/genesis.json --inet4-only
```

**Addrbook:** ```https://desmos.declab.pro/addrbook.json```

```
wget -O ~/.desmos/config/addrbook.json https://desmos.declab.pro/addrbook.json --inet4-only
```

**Peer:** ```73ef1c0f9bc77fd925decf7fa41f22a35b5dc76d@desmos.declab.pro:26615```

```
PEERS=73ef1c0f9bc77fd925decf7fa41f22a35b5dc76d@desmos.declab.pro:26615
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.desmos/config/config.toml
```

## Snapshot 

**Link:** ```https://desmos.declab.pro/latest.tar.lz4```

```
# Reset tendermint chain
desmos tendermint unsafe-reset-all

# Download and unpack the archive
curl -o - -L https://desmos.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C ~/.desmos
```

## State sync

```
RPC="https://desmos.declab.pro:26613"

LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" ~/.desmos/config/config.toml
```
