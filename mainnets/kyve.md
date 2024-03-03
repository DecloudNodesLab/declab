# Kyve (Chain mainnet node)

![](/assets/banner.png)

|[Site](https://www.kyve.network/)|[Discord](https://discord.gg/PATvZvEmxF)|[Github](https://github.com/KYVENetwork)|
|:--:|:--:|:--:|
|[Medium](https://blog.kyve.network/)|[Youtube](https://www.youtube.com/channel/UCThrQRlVd2KKy2-e0tBgfpQ)|[X](https://twitter.com/KYVENetwork)|
|[Guide](https://services.declab.pro/guides)|[Deploy file](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects/Kyve/kyve_deploy.yml)|[Delegate to us](https://restake.app/kyve/kyvevaloper1ax4c40gn3s74xxm75g6cmts3fw7rq64gzgc27r)|


[Kyve EXPLORER](https://explorer.declab.pro/Kyve)|
|:--:|

## Endpoints

|[**RPC**](https://kyve.declab.pro:26631)|[**API**](https://kyve.declab.pro)|
|:--:|:--:|

**Genesis:** ```https://kyve.declab.pro/genesis.json```

```
wget -O ~/.kyve/config/genesis.json https://kyve.declab.pro/genesis.json --inet4-only
```

**Addrbook:** ```https://kyve.declab.pro/addrbook.json```

```
wget -O ~/.kyve/config/addrbook.json https://kyve.declab.pro/addrbook.json --inet4-only
```

**Peer:** ```73ef1c0f9bc77fd925decf7fa41f22a35b5dc76d@kyve.declab.pro:26633```

```
PEERS=73ef1c0f9bc77fd925decf7fa41f22a35b5dc76d@kyve.declab.pro:26633
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.kyve/config/config.toml
```

## Snapshot 

**Link:** ```https://kyve.declab.pro/latest.tar.lz4```

```
# Reset tendermint chain
kyved tendermint unsafe-reset-all

# Download and unpack the archive
curl -o - -L https://kyve.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C ~/.kyve
```

## State sync

```
RPC="https://kyve.declab.pro:26631"

LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" ~/.kyve/config/config.toml
```
