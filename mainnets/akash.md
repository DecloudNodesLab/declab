# Akash Network

![](/assets/banner.png)

|[Akash site](https://akash.network/)|[Akash Discord](https://discord.akash.network/)|[Akash Github](https://github.com/akash-network)|
|:--:|:--:|:--:|
|[Akash Telegram EN](https://t.me/AkashNW)|[Akash Telegram RU](https://t.me/akash_ru)|[Akash X](https://twitter.com/akashnet_)|
|[Guide](https://services.declab.pro/guides)|[Deploy file](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects/Akash_Network/akash_mainnet_deploy.yml)|[Delegate to us](https://restake.app/akash/akashvaloper1ax4c40gn3s74xxm75g6cmts3fw7rq64gq0kaj4a)|


## Endpoints

|[**RPC**](https://akash.declab.pro:26601)|[**API**](https://akash.declab.pro)|
|:--:|:--:|

**Genesis:** ```https://akash.declab.pro/genesis.json```

```
wget -O genesis.json https://akash.declab.pro/genesis.json --inet4-only
mv genesis.json ~/.akash/config
```

**Addrbook:** ```https://akash.declab.pro/addrbook.json```

```
wget -O addrbook.json https://akash.declab.pro/addrbook.json --inet4-only
mv addrbook.json ~/.akash/config
```

**Peer:** ```d85b6e290e57701f5b816baa01b6a286c14f9400@akash.declab.pro:26606```

```
PEERS=d85b6e290e57701f5b816baa01b6a286c14f9400@akash.declab.pro:26606,064b1c1a295ca9b3a1360283086f61705525aeed@192.175.53.243:26656,b9751d5a8b3c2f242b5de21c3d5ff6440d8765cd@52.30.142.144:26656,f31426d9fb39c2d97653722a34b4c72db71904c2@93.115.25.106:29656,37201c92625df2814a55129f73f10ab6aa2edc35@95.214.53.215:26696,34aa700c44f35abe8319428f173503ea7faee3b7@144.76.56.87:28656
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.akash/config/config.toml
```

## Snapshot 

**Link:** ```https://akash.declab.pro/latest.tar.lz4```

```
# Reset tendermint chain
akash tendermint unsafe-reset-all

# Download and unpack the archive
curl -o - -L https://akash.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C ~/.akash
```

## State sync

```
RPC="https://akash.declab.pro:26601"

LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" ~/.akash/config/config.toml
```
