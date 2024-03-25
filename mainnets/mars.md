# Mars Protocol

![](/assets/banner.png)

|[Mars site](https://marsprotocol.io/)|[Mars Discord](https://discord.marsprotocol.io/)|[Mars Github](https://github.marsprotocol.io/)|
|:--:|:--:|:--:|
|[Mars Telegram](https://telegram.marsprotocol.io/)|[Mars Youtube](https://youtube.marsprotocol.io/)|[Mars X](https://twitter.marsprotocol.io/)|
|[Guide](https://services.declab.pro/guides)|[Deploy file](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects/Mars/mars_mainnet_deploy.yml)|[Delegate to us](https://restake.app/mars/marsvaloper1ax4c40gn3s74xxm75g6cmts3fw7rq64gw8ss2m)|


[Mars EXPLORER](https://explorer.declab.pro/Mars)|
|:--:|


## Endpoints

|[**RPC**](https://mars.declab.pro:26634)|[**API**](https://mars.declab.pro:443)|
|:--:|:--:|

**Genesis:** ```https://mars.declab.pro/genesis.json```

```
wget -O ~/.mars/config/genesis.json https://mars.declab.pro/genesis.json --inet4-only
```

**Addrbook:** ```https://mars.declab.pro/addrbook.json```

```
wget -O ~/.mars/config/addrbook.json https://mars.declab.pro/addrbook.json --inet4-only
```

**Peer:** ```73ef1c0f9bc77fd925decf7fa41f22a35b5dc76d@mars.declab.pro:26636```

```
PEERS=73ef1c0f9bc77fd925decf7fa41f22a35b5dc76d@mars.declab.pro:26636,f321c169758c76c213094a58af13365774bf181c@57.128.95.94:26656,e1b058e5cfa2b836ddaa496b10911da62dcf182e@134.65.193.187:26656,305d93229a89ae46265ef08536aa962d4a0dee67@65.108.131.18:26656,f025e2e0e2e0e432d38546e1b95153de7eadf4a1@213.246.39.89:11656,469d7b65474cdd14aaa5e47c83934ce2a7445d82@3.217.47.126:26656
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.mars/config/config.toml
```

## Snapshot 

**Link:** ```https://mars.declab.pro/latest.tar.lz4```

```
# Reset tendermint chain
akash tendermint unsafe-reset-all

# Download and unpack the archive
curl -o - -L https://mars.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C ~/.mars
```

## State sync

```
RPC="https://mars.declab.pro:26634"

LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" ~/.mars/config/config.toml
```
