# Gitopia

![](/assets/banner.png)

|[Site](https://gitopia.com/)|[Discord](https://discord.gg/QGBCkdSZ)|[Repository](https://gitopia.com/home)|
|:--:|:--:|:--:|
|[Telegram](https://t.me/Gitopia)|[Medium](https://gitopia.com/gitopia/gitopia-docs)|[X](https://twitter.com/gitopiaDAO)|
|[Guide](https://services.declab.pro/guides)|[Deploy file](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects/Gitopia/gitopia_mainnet_deploy.yml)|[Delegate to us](https://restake.app/gitopia/gitopiavaloper1nuphu4p06dlgx2se0w58z5c7yv00r5gl37qcrm)|

[Gitopia EXPLORER](https://explorer.declab.pro/Gitopia)|
|:--:|

## Endpoints

|[**RPC**](https://gitopia.declab.pro:26625)|[**API**](https://gitopia.declab.pro)|
|:--:|:--:|

**Genesis:** ```https://gitopia.declab.pro/genesis.json```

```
wget -O  ~/.gitopia/config/genesis.json https://gitopia.declab.pro/genesis.json --inet4-only
```

**Addrbook:** ```https://gitopia.declab.pro/addrbook.json```

```
wget -O ~/.gitopia/config/addrbook.json https://gitopia.declab.pro/addrbook.json --inet4-only
```

**Peer:** ```73ef1c0f9bc77fd925decf7fa41f22a35b5dc76d@gitopia.declab.pro:26627```

```
PEERS=73ef1c0f9bc77fd925decf7fa41f22a35b5dc76d@gitopia.declab.pro:26627,c35eb6124591bad21673e8d802898faa18e0352a@65.109.29.150:36656,a0b6c89b4fe0f455a027080103bffd001f3b6248@65.21.134.202:26356,e46b53a03cc5d369f743f049618517da7902cc50@147.135.31.22:11356,fbeb3707a4313bb06e89cfb08864ed2582eb7e47@65.108.141.109:30656,7324256048dd091bb1905b4bcda888d79d3592c5@103.180.28.90:26656
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.gitopia/config/config.toml
```

## Snapshot 

**Link:** ```https://gitopia.declab.pro/latest.tar.lz4```

```
# Reset tendermint chain
gitopiad tendermint unsafe-reset-all

# Download and unpack the archive
curl -o - -L https://gitopia.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C ~/.gitopia
```

## State sync

```
RPC="https://gitopia.declab.pro:26625"

LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" ~/.gitopia/config/config.toml
```
