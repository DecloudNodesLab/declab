# Realio Network

![](/assets/banner.png)

|[Site](https://realio.network/)|[Discord](https://discord.gg/56db5TARck)|[Github](https://github.com/realiotech)|
|:--:|:--:|:--:|
|[Blog](https://www.realio.fund/blog)|[Linkedin](https://www.linkedin.com/company/realio)|[X](https://twitter.com/realio_network)|
|[Guide](https://services.declab.pro/guides)|[Deploy file](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects/Realio/realio_deploy.yml)|[Delegate to us](https://restake.app/realio/realiovaloper1chee8l82uxqfduxr8x0pfrp9psl08cy4a20m0u)|


[Realio Network EXPLORER](https://explorer.declab.pro/Realio)|
|:--:|

## Endpoints

|[**RPC**](https://realio.declab.pro:26622)|[**API**](https://realio.declab.pro)|
|:--:|:--:|

**Genesis:** ```https://realio.declab.pro/genesis.json```

```shell
wget -O ~/.realio-network/config/genesis.json https://realio.declab.pro/genesis.json --inet4-only
```

**Addrbook:** ```https://realio.declab.pro/addrbook.json```

```shell
wget -O ~/.realio-network/config/addrbook.json https://realio.declab.pro/addrbook.json --inet4-only
```

**Peer:** ```73ef1c0f9bc77fd925decf7fa41f22a35b5dc76d@realio.declab.pro:26624```

```shell
PEERS=73ef1c0f9bc77fd925decf7fa41f22a35b5dc76d@realio.declab.pro:26624
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.realio-network/config/config.toml
```

## Snapshot 

**Link:** ```https://realio.declab.pro/latest.tar.lz4```

```shell
# Reset tendermint chain
realio-networkd tendermint unsafe-reset-all

# Download and unpack the archive
curl -o - -L https://realio.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C ~/.realio-network
```

## State sync

```shell
RPC="https://realio.declab.pro:26622"

LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" ~/.realio-network/config/config.toml
```
