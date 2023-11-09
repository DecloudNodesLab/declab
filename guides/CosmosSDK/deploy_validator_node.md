<p align="center"><img src="https://user-images.githubusercontent.com/23629420/219872517-2adc32b1-5f64-4d48-9a81-1e2ef6b01a53.png" </p>
  
<div align="center">  
  
|[Decloud Nodes Lab](https://declab.pro)|[Discord Decloud Nodes Lab](https://discord.gg/eDKdvjfUAS)|[Twitter Decloud Nodes Lab](https://twitter.com/NodesLab)|
|:--:|:--:|:--:|

</div>

# Validator node deployment on Akash Network.

___

## Node deployment:

Select a project and deploy the [deploy.yml](https://gitopia.com/DecloudNodesLab/cosmos-universe/tree/master/projects) file using **Cloudmos** ([instructions for use here](https://docs.declab.pro/guides/cloudmos)).
If you use the projects that we have prepared, then you just need to enter your values in the variables listed below in `deploy.yml`, leave the rest unchanged: <br/>
```
- "SSH_KEY=" - Public ssh-key for connecting via SSH (user root). If it is not specified, the SSH service will not be installed.
- "MONIKER=" - Node name.
- "VALIDATOR_KEY_JSON_BASE64=" - Paste the contents of the priv_validator_key.json file encrypted with BASE64 *.
```
> If you want to deploy an **RPC** node without a validator key - missing delete this environment VALIDATOR_KEY_JSON_BASE64. The node runs on the generated `priv_validator_key.json`.

If you deployed the project node yourself, then here is a list of available environment in `deploy.yml`: <br/>
```
- "GITHUB_REPOSITORY=" - Link to the project repository that will be cloned into the container and inside which
                           getting a compilation of a binary file.
- "BINARY_LINK=" link to compiled binary file or archive with it.*
- "BINARY_VERSION=" The version or commit of the binary you want to compile (can only use
                      with GITHUB_REPOSITORY populated).
- "RPC=" - External RPC node used to check STATE SYNC, find effective peers, read GENESIS file.
- "GENESIS=" - Link to genesis.json file. With this capability, reading from RPC will be disabled.
- "PEERS=" - Enter a list of peers separated by commas, in this case, automatic search will be disabled.
- "SEEDS=" - Enter a list of seeds separated by commas.
- "DENOM=" - Manual setting of the nominal value of the token.
- "CHAIN=" - Manual setting of chain-id.
- "STATE_SYNC=enable" - enable state sync(disable default).
- "SNAPSHOT=" - Link to lz4 network snapshot archive. Use in conjunction with STATE_SYNC=off.
* When building BINARY_LINK, you must add a BINARY variable - containing the name
binary file.

```
If you don't have `priv_validator_key.json`, refer to [this manual](https://docs.declab.pro/guides/cosmos-sdk/create_validator_key).

By going to the forwarded port **26657**, in the `LEASES` tab, you can view `websocket` of the node, where its up-to-date information was available.

<div align="center">

<p align="center"><img src="https://github.com/DecloudNodesLab/declab/assets/23629420/046ff147-7765-4e78-b3c8-dd407cd5dce8" width=45% align="left"</p>
<p align="center"><img src="https://user-images.githubusercontent.com/23629420/182032818-069eef95-8242-459f-b503-ad8322261482.png" width=45% </p>

</div>

**Thank you for using Akash Network!**
___
