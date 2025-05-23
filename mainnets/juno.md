# Juno

![](/assets/banner.png)

|[Site](https://www.junonetwork.io/)|[Discord](https://discord.gg/mcHpbvjYBA)|[Github](https://github.com/CosmosContracts)|
|:--:|:--:|:--:|
|[Telegram](https://t.me/JunoNetwork)|[Medium](https://docs.junonetwork.io/juno/readme)|[X](https://twitter.com/JunoNetwork)|
|[Guide](https://services.declab.pro/guides)|[Deploy file](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects/Juno/juno_deploy.yml)|[Delegate to us](https://restake.app/juno/junovaloper1ax4c40gn3s74xxm75g6cmts3fw7rq64gweqg8q)|


[Juno EXPLORER](https://explorer.declab.pro/Juno)|
|:--:|

## Endpoints

|[**RPC**](https://juno.declab.pro:26610)|[**API**](https://juno.declab.pro)|
|:--:|:--:|

**Genesis:** ```https://juno.declab.pro/genesis.json```

```shell
wget -O ~/.juno/config/genesis.json https://juno.declab.pro/genesis.json --inet4-only
```

**Addrbook:** ```https://juno.declab.pro/addrbook.json```

```shell
wget -O  ~/.juno/config/addrbook.json https://juno.declab.pro/addrbook.json --inet4-only
```

**Peer:** ```ba988720e05afdcea922130e3f3af23960c285dd@juno.declab.pro:26612```

```shell
PEERS=ba988720e05afdcea922130e3f3af23960c285dd@juno.declab.pro:26612,0edf09d33c9f5429c7539f11a56e1e0ab8981529@144.217.158.129:26656,07191cd1f1968bd21373b53eb5b932deb408a5b7@167.235.216.230:27003,b1d278873767fad599ebf710f840d90c93e8caeb@95.111.249.160:26656,839088f5507a45d1cee03739f741d87749868009@198.244.165.175:16656,7b4cd4197afd6851abdf0875bfb3e348df8b03cc@65.109.61.50:26656
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.juno/config/config.toml
```

## Snapshot 

**Link:** ```https://juno.declab.pro/snapshot.tar.lz4```

```shell
# Reset tendermint chain
junod tendermint unsafe-reset-all

# Download and unpack the archive
curl -o - -L https://juno.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C ~/.juno
```

## State sync

```shell
RPC="https://juno.declab.pro:26610"

LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" ~/.juno/config/config.toml
```
