# Vidulum

![](/assets/banner.png)

|[Site](https://vidulum.app/)|[Discord](https://discord.gg/hne7Ccq)|[Github](https://github.com/vidulum)|
|:--:|:--:|:--:|
|[Youtube](https://www.youtube.com/channel/UCNd92ZViZweu6zz5ydt_wrQ)|[Reddit](https://www.reddit.com/r/VidulumOfficial/)|[X](https://twitter.com/VidulumApp)|
|[Guide](https://services.declab.pro/guides)|[Deploy file](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects/Vidulum/vidulum_deploy.yml)|[Delegate to us](https://restake.app/vidulum/vdlvaloper1nuphu4p06dlgx2se0w58z5c7yv00r5gle0h5gs)|

[Vidulum EXPLORER](https://explorer.declab.pro/Vidulum)|
|:--:|

## Endpoints

|[**RPC**](https://vidulum.declab.pro:26625)|[**API**](https://vidulum.declab.pro)|
|:--:|:--:|

**Genesis:** ```https://vidulum.declab.pro/genesis.json```

```
wget -O ~/.vidulum/config/genesis.json https://vidulum.declab.pro/genesis.json --inet4-only
```

**Addrbook:** ```https://vidulum.declab.pro/addrbook.json```

```
wget -O ~/.vidulum/config/addrbook.json https://vidulum.declab.pro/addrbook.json --inet4-only
```

**Peer:** ```73ef1c0f9bc77fd925decf7fa41f22a35b5dc76d@vidulum.declab.pro:26627```

```
PEERS=73ef1c0f9bc77fd925decf7fa41f22a35b5dc76d@vidulum.declab.pro:26627,8ec095406fe54cb951b537efc62e01d462af97f6@37.187.149.93:26706, 52051fef449e76eb399966312f523e8e5e27490b@95.217.118.211:26656, 4705f4510963433268cf85e5a8923b6e7b07de1e@208.77.197.82:28656, 7e06f509284dc6cc0bf2234685667fa54232a28c@149.248.56.74:26656, 695606292191d387ec52e38a92f6e8250c43c390@65.108.136.206:26656, 25c5d495e6f943b81b4344b64ca62a256ebc1e70@66.45.231.30:11434, 182389e2eb31d5b820d8ed99d12d60726eea8d3f@65.21.122.47:29656, 0235adf78ddfcecff335e83ace4bfb33af65680e@162.19.139.218:26656, 844c07cb557529c5e1ce2005028986fd364fd386@73.117.148.143:26656, 4379a9a8eecadff7f92e2899d74b82a6f030bb8b@23.146.184.45:26656, bfdaa4bc2d76de9e59b8447e73e8bfccb3526f38@103.19.25.132:26656, 1d3beff50d0ffc6793689446fe263ee428681fdb@109.70.113.100:46656, aedd3fbe7c7f9592a91647f202beaa8639e70ca2@94.250.203.6:22656, fa1144b7a13a93660206d30f4f9e45d3dffe5087@136.38.121.78:26656, cd2827f964ced1a9ce888d48a92b300684f89ecb@65.108.121.190:2050, 66083f6818ee6bcd432dd8946fc558c85f6de9f6@174.138.172.50:41656, ae7c8f6c7540471841eb5115411d9ca3eaea4113@185.237.252.152:26656, 1b9d18398278559d5305c2048ea6e5558b6ba176@169.0.112.239:26656, 8676c869a6726fe94269d63af88645cab4b74aaf@68.142.182.44:26656, 9417154d9a5fa48fe72621d9e9b74409504f72e3@65.108.11.250:28656, 341cc1e9ac51013ba9bd4eb8ae3fed4962ec5961@88.198.24.4:26656, f9841439039fecaa04fc4c951191eebc6ea10cf2@135.181.6.244:26656, 7a1c728720d05e48f17fc37d3ff990fd91feab93@167.114.118.234:26806, 62c43e6a3616851922bfeeffec1dd8e4ddbc9bd3@192.99.4.66:26806, d3ef1a3a138fdeaa3fadad6cf3b8c76e77a08c00@108.61.217.185:26656, 9b06813ff7e4536daac7e0c63dd0441741ace0ea@185.217.127.76:26656, 209688f5bccb88f6397a97cc11ab545a014aa559@137.184.92.115:26656, 3bd358f867ae446360078049c93b24fe2e317d65@65.108.142.240:26640, 057fa262fe2030cc6e9095dc52d15b79ffcb923d@142.115.20.25:26656, 564086e64b559fc992e4befa8bbc27b75cf88b94@45.134.226.92:26656, 1f0bcfce2def9553c2a2f64342927a495ac27a38@144.202.60.139:443, 3bf3d98dfd4000dd5ff8189882a9f96848b99b87@45.63.57.251:26656, 7a44ea6ecb59b0e4bd01b58a75163ec64b164bb4@63.210.148.24:26656, d8124f45b366816a55129531b97f3bdb294a75eb@73.40.151.121:46656
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/.vidulum/config/config.toml
```

## Snapshot 

**Link:** ```https://vidulum.declab.pro/latest.tar.lz4```

```
# Reset tendermint chain
vidulumd tendermint unsafe-reset-all

# Download and unpack the archive
curl -o - -L https://vidulum.declab.pro/latest.tar.lz4 | lz4 -c -d - | tar -x -C ~/.vidulum
```

## State sync

```
RPC="https://vidulum.declab.pro:26625"

LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" ~/.vidulum/config/config.toml
```
