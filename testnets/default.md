# Project name

|[Site]()|[Discord]()|[Github]()|
|:--:|:--:|:--:|
|[Telegram]()|[Medium]()|[X]()|
|[Guide](https://services.declab.pro/guides)|[Deploy file]()|[Delegate to us]()|


## Endpoints

**Genesis:** ```https://.declab.pro/genesis.json```

**Addrbook:** ```https://.declab.pro/addrbook.json```

**RPC:** ```https://.declab.pro/rpc```

**API:** ```https://.declab.pro```

**Peer:** ```ID@ADDRESS:PORT```

```
PEERS=
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.FOLDER/config/config.toml
```

## Snapshot 

**Link:** ```https://.declab.pro/latest.tar.lz4```

```
# Reset tendermint chain
BINARY tendermint unsafe-reset-all

# Download and unpack the archive
curl -o - -L https://.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.FOLDER
```

## State sync

```
RPC="ADDRESS:PORT"

LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.FOLDER/config/config.toml
```
