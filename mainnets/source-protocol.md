# Source Protocol

|[Site](https://www.sourceprotocol.io/)|[Discord](https://discord.gg/VbwdjqYjzr)|[Github](https://github.com/Source-Protocol-Cosmos)|
|:--:|:--:|:--:|
|[Telegram](https://t.me/SourceProtocol)|[Medium](https://docs.sourceprotocol.io/)|[X](https://twitter.com/SourceProtocol_)|
|[Guide](https://services.declab.pro/guides)|[Deploy file](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects/Source/source_mainnet_deploy.yml)|[Delegate to us](https://restake.app/source/sourcevaloper126erf9dmm4e3fs0suk9lnv24wudswkm3ekfqfh)|


## Endpoints

**Genesis:** ```https://source.declab.pro/genesis.json```

**Addrbook:** ```https://source.declab.pro/addrbook.json```

**RPC:** ```https://source.declab.pro/rpc```

**API:** ```https://source.declab.pro```

**Peer:** ```a3ec1436a7645cf40ac9e1389e4035367be2da1f@provider.dcnorse.ddns.net:30576```

```
PEERS=a3ec1436a7645cf40ac9e1389e4035367be2da1f@provider.dcnorse.ddns.net:305765954580c1fdb1faddd834a1632d495186e1cb06f@75.119.146.181:26656,8b7fd04ce47825b030daf93a20ed63a5422c6471@65.109.94.250:30656,0107ac60e43f3b3d395fea706cb54877a3241d21@35.87.85.162:26656,94ddb595c7a4cca5bc9d8026b310837db5fdb261@54.90.73.200:26656,79adf04741f4a019684efc73e42467cb7d6d3a69@148.251.19.41:25656
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.source/config/config.toml
```

## Snapshot 

**Link:** ```https://source.declab.pro/latest.tar.lz4```

```
# Reset tendermint chain
sourced tendermint unsafe-reset-all

# Download and unpack the archive
curl -o - -L https://source.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.source
```

## State sync

```
RPC="http://provider.dcnorse.ddns.net:30293"

LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.source/config/config.toml
```
