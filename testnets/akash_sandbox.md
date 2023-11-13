# Akash Network

|[Akash site](https://akash.network/)|[Akash Discord](https://discord.akash.network/)|[Akash Github](https://github.com/akash-network)|
|:--:|:--:|:--:|
|[Akash Telegram EN](https://t.me/AkashNW)|[Akash Telegram RU](https://t.me/akash_ru)|[Akash X](https://twitter.com/akashnet_)|
|[Guide](https://services.declab.pro/guides)|[Deploy file](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects/Akash_Network/akash_sandbox_deploy.yml)|[Delegate to us](https://restake.app/akash/akashvaloper1ax4c40gn3s74xxm75g6cmts3fw7rq64gq0kaj4a)|


## Endpoints

|[**RPC**](https://akash-sandbox.declab.pro/rpc)|[**API**](https://akash-sandbox.declab.pro)|
|:--:|:--:|

**Genesis:** ```https://akash-sandbox.declab.pro/genesis.json```

```
wget -O genesis.json https://akash-sandbox.declab.pro/genesis.json --inet4-only
mv genesis.json ~/.akash/config
```

**Addrbook:** ```https://akash-sandbox.declab.pro/addrbook.json```

```
wget -O addrbook.json https://akash-sandbox.declab.pro/addrbook.json --inet4-only
mv addrbook.json ~/.akash/config
```

**Peer:** ```d85b6e290e57701f5b816baa01b6a286c14f9400@provider.palmito.duckdns.org:30637```

```
PEERS=d85b6e290e57701f5b816baa01b6a286c14f9400@provider.palmito.duckdns.org:30637,e06a303953a66de205d35e6ab1f17c0dc035a516@p2p.sandbox-01.aksh.pw:26656,df9dbde281cc2b64137423f9fabac9f0ef70b3bc@104.21.78.218:30592,178aceed035d9310482bc42e0aa1c0e4af7693e8@162.55.245.144:12010
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.akash/config/config.toml
```

## Snapshot 

**Link:** ```https://akash-sandbox.declab.pro/latest.tar.lz4```

```
# Reset tendermint chain
akash tendermint unsafe-reset-all

# Download and unpack the archive
curl -o - -L https://akash-sandbox.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.akash
```

## State sync

```
RPC="http://provider.palmito.duckdns.org:30760"

LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.akash/config/config.toml
```
