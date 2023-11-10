# Gitopia

|[Site](https://gitopia.com/)|[Discord](https://discord.gg/QGBCkdSZ)|[Repository](https://gitopia.com/home)|
|:--:|:--:|:--:|
|[Telegram](https://t.me/Gitopia)|[Medium](https://gitopia.com/gitopia/gitopia-docs)|[X](https://twitter.com/gitopiaDAO)|
|[Guide](https://services.declab.pro/guides)|[Deploy file](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects/Gitopia/gitopia_mainnet_deploy.yml)|[Delegate to us](https://restake.app/gitopia/gitopiavaloper1nuphu4p06dlgx2se0w58z5c7yv00r5gl37qcrm)|


## Endpoints

**Genesis:** ```https://gitopia.declab.pro/genesis.json```

**Addrbook:** ```https://gitopia.declab.pro/addrbook.json```

**RPC:** ```https://gitopia.declab.pro/rpc```

**API:** ```https://gitopia.declab.pro```

**Peer:** ```1f08f14bdd7076e9fdd3a8b7b94eca20366c7be5@provider.nmfakash.uk:30235```

```
PEERS=1f08f14bdd7076e9fdd3a8b7b94eca20366c7be5@provider.nmfakash.uk:30235,4ffa0ea96f12080e74c53ca9f8aaf4390bab4bb1@138.201.204.5:48656,5dd42aa52e4f0e7bb89404ad6b919f0b9870f917@37.252.184.245:26656,901c393d17c1e6094cbbc83c34f167a67bb5fab1@65.108.70.119:36656,967f46c329db6cff79903a101c655f85f8a18536@212.23.222.220:26256,0ba4bc31b06a7e22f3574e853ef9f51835e920ce@144.76.174.27:26656
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.gitopia/config/config.toml
```

## Snapshot 

**Link:** ```https://gitopia.declab.pro/latest.tar.lz4```

```
# Reset tendermint chain
gitopiad tendermint unsafe-reset-all

# Download and unpack the archive
curl -o - -L https://gitopia.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.gitopia
```

## State sync

```
RPC="http://provider.nmfakash.uk:32537"

LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.gitopia/config/config.toml
```
