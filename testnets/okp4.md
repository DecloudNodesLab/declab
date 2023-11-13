# OKP4

|[OKP4 Site](https://okp4.network/)|[Discord](https://discord.gg/okp4)|[Github](https://github.com/okp4)|
|:--:|:--:|:--:|
|[Telegram](https://t.me/okp4network)|[Medium](https://blog.okp4.network/)|[X](https://twitter.com/OKP4_Protocol)|
|[Guide](https://services.declab.pro/guides)|[Deploy file](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects/OKP4/okp4_deploy.yml)|[Documentations](https://docs.okp4.network/)|


## Endpoints

|[**RPC**](https://okp4.declab.pro/rpc)|[**API**](https://okp4.declab.pro)|
|:--:|:--:|

**Genesis:** ```https://okp4.declab.pro/genesis.json```

```
wget -O genesis.json https://okp4.declab.pro/genesis.json --inet4-only
mv genesis.json ~/.okp4d/config
```

**Addrbook:** ```https://okp4.declab.pro/addrbook.json```

```
wget -O addrbook.json https://okp4.declab.pro/addrbook.json --inet4-only
mv addrbook.json ~/.okp4d/config
```

**Peer:** ```d85b6e290e57701f5b816baa01b6a286c14f9400@provider.d3akash.cloud:32164```

```
PEERS=d85b6e290e57701f5b816baa01b6a286c14f9400@provider.d3akash.cloud:32164,f7e481df45bfbe62ea0553f5f6da34eaf4f688c3@194.34.232.225:26656,3c805c2dead7b7a3a1d3ba2399d4d62153322413@65.108.2.41:36656,854cc8b83a48ba4394c1940b57d0f42ec013e033@38.242.251.204:26656,a98484ac9cb8235bd6a65cdf7648107e3d14dab4@116.202.231.58:13656,f045c5324e03d54f96285a33130d3886457e18be@46.4.81.204:49656
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.okp4d/config/config.toml
```

## Snapshot 

**Link:** ```https://okp4.declab.pro/latest.tar.lz4```

```
# Reset tendermint chain
BINARY tendermint unsafe-reset-all

# Download and unpack the archive
curl -o - -L https://okp4.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.okp4d
```

## State sync

```
RPC="provider.d3akash.cloud:31296"

LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.okp4d/config/config.toml
```
