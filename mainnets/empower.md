# Empower

![](/assets/banner.png)

|[Site](https://www.empowerchain.io/)|[Discord](https://discord.com/invite/DNB4z8EZDx)|[Github](https://github.com/EmpowerPlastic)|
|:--:|:--:|:--:|
|[Telegram](https://t.me/empowerchain)|[Medium](https://docs.empowerchain.io/)|[X](https://twitter.com/empowerchain_io)|
|[Guide](https://services.declab.pro/guides)|[Deploy file](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects/Empower/empower_mainnet.yml)|[Delegate to us](https://restake.app/empowerchain/empowervaloper1ax4c40gn3s74xxm75g6cmts3fw7rq64grp0c0w)|

[Empower EXPLORER](https://explorer.declab.pro/Empower)|
|:--:|

## Endpoints

|[**RPC**](https://empower.declab.pro:26607)|[**API**](https://empower.declab.pro)|
|:--:|:--:|

**Genesis:** ```https://empower.declab.pro/genesis.json```

```shell
wget -O  ~/.empowerchain/config/genesis.json https://empower.declab.pro/genesis.json --inet4-only
```

**Addrbook:** ```https://empower.declab.pro/addrbook.json```

```shell
wget -O ~/.empowerchain/config/addrbook.json https://empower.declab.pro/addrbook.json --inet4-only
```

**Peer:** ```73ef1c0f9bc77fd925decf7fa41f22a35b5dc76d@empower.declab.pro:26609```

```shell
PEERS=73ef1c0f9bc77fd925decf7fa41f22a35b5dc76d@empower.declab.pro:26609,bb8f0eb3ce0e8ad9043f884db42865cfd293851f@81.0.218.135:21956,901ce8eedf012ec5c74bf040f4901a42e4c66e0c@142.132.193.194:26656,ee0973d050e077a2f8cb7e90969560b0fe255929@148.113.159.22:17456,1ad467e3c21a7c30a9e1dc68166570f40b467cad@151.80.27.157:26656,f7eb23352efa7aba7ba9aa56fe034ede139deab3@65.109.116.119:16856
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.empowerchain/config/config.toml
```

## Snapshot 

**Link:** ```https://empower.declab.pro/latest.tar.lz4```

```shell
# Reset tendermint chain
empowerd tendermint unsafe-reset-all
# Download and unpack the archive
curl -o - -L https://empower.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C ~/.empowerchain
```

## State sync

```shell
RPC="https://empower.declab.pro:26607"
LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" ~/.empowerchain/config/config.toml
```
