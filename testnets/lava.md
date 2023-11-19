# Lava Network

![](/assets/banner.png)

|[Lava Site](https://www.lavanet.xyz/)|[Discord](https://discord.gg/Tbk5NxTCdA)|[Github](https://github.com/lavanet)|
|:--:|:--:|:--:|
|[Documentations](https://docs.lavanet.xyz/)|[Gateway](https://accounts.lavanet.xyz/)|[X](https://twitter.com/lavanetxyz)|
|[Guide](https://services.declab.pro/guides)|[Deploy file](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects/Lava/lava_testnet_deploy.yml)|[Lava Dashboard](https://info.lavanet.xyz/)|


## Endpoints

|[**RPC**](https://lava.declab.pro/rpc)|[**API**](https://lava.declab.pro)|
|:--:|:--:|

**Genesis:** ```https://lava.declab.pro/genesis.json```

```
wget -O genesis.json https://lava.declab.pro/genesis.json --inet4-only
mv genesis.json ~/.lava/config
```

**Addrbook:** ```https://lava.declab.pro/addrbook.json```

```
wget -O addrbook.json https://lava.declab.pro/addrbook.json --inet4-only
mv addrbook.json ~/.lava/config
```

**Peer:** ```d85b6e290e57701f5b816baa01b6a286c14f9400@provider.nmfakash.uk:32005```

```
PEERS=85b6e290e57701f5b816baa01b6a286c14f9400@provider.nmfakash.uk:32005,c3bcd6779abf9bc703ff89d72f9aa91dc4b3068e@65.21.131.21:26656,40046fe63bdaa9efde27707b0d3de0bf84fedf80@86.111.48.158:26656,0d6983bcd192c0b4a0f61e6d849c152704e2f017@91.107.148.5:26656,3031bcee46e31081eb6ecb90df2dad6fc757bebc@95.217.57.232:56656,b3abed4b1ad82a3d2404c817b4eabf30ab36f6f6@185.250.36.187:17656
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.lava/config/config.toml
```

## Snapshot 

**Link:** ```https://lava.declab.pro/latest.tar.lz4```

```
# Reset tendermint chain
BINARY tendermint unsafe-reset-all

# Download and unpack the archive
curl -o - -L https://lava.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.lava
```

## State sync

```
RPC="https://provider.nmfakash.uk:31128"

LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.lava/config/config.toml
```
