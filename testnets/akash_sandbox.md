# Akash Network

|[Akash site](https://akash.network/)|[Akash Discord](https://discord.akash.network/)|[Akash Github](https://github.com/akash-network)|
|:--:|:--:|:--:|
|[Akash Telegram EN](https://t.me/AkashNW)|[Akash Telegram RU](https://t.me/akash_ru)|[Akash X](https://twitter.com/akashnet_)|
|[Guide](https://services.declab.pro/guides)|[Deploy file](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects/Akash_Network/akash_sandbox_deploy.yml)|[Delegate to us](https://restake.app/akash/akashvaloper1ax4c40gn3s74xxm75g6cmts3fw7rq64gq0kaj4a)|


## Endpoints

**Genesis:** ```https://akash-sandbox.declab.pro/genesis.json```

**Addrbook:** ```https://akash-sandbox.declab.pro/addrbook.json```

**RPC:** ```https://akash-sandbox.declab.pro/rpc```

**API:** ```https://akash-sandbox.declab.pro```

**Peer:** ```a8d94ea78624d3559d6df3e31c6a884ee55439e2@provider.dcnorse.ddns.net:31848```

```
PEERS=a8d94ea78624d3559d6df3e31c6a884ee55439e2@provider.dcnorse.ddns.net:31848,e06a303953a66de205d35e6ab1f17c0dc035a516@p2p.sandbox-01.aksh.pw:26656,df9dbde281cc2b64137423f9fabac9f0ef70b3bc@104.21.78.218:30592,178aceed035d9310482bc42e0aa1c0e4af7693e8@162.55.245.144:12010
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
RPC="http://provider.dcnorse.ddns.net:30424"

LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.akash/config/config.toml
```
