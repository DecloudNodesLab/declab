# Deploy V2RAY vpn server on Akash Network

![image](https://user-images.githubusercontent.com/23629420/219872517-2adc32b1-5f64-4d48-9a81-1e2ef6b01a53.png)

**Product documentation:**

| [Site V2RAY](https://www.v2fly.org/en_US) | [GitHub V2RAY](https://github.com/v2fly) |
|:--:|:--:|

## Step 1 (Create and share your config.json)

You can use example [config.json](https://gitopia.com/DecloudNodesLab/software/tree/master/v2ray/example_config.json), replacing the `ID` ( [generator UUID](https://www.uuidgenerator.net/) ) in the file to have your id.
Or create your own `config.json` by going to the [documentation](https://www.v2fly.org/en_US/guide/start.html).
Place your `config.json` file on any platform where direct download will be available (github, google drive, etc.).

## Step 2 (Deploy on Akash Network)

Deploy [deploy.yml](https://gitopia.com/DecloudNodesLab/software/tree/master/v2ray/deploy.yml) file on Akash Network. If need, replace with your own link, the value in the `CONFIG_LINK` variable. Select provider and waiting finish deploy.

![image](https://github.com/DecloudNodesLab/Projects/assets/23629420/9a72129d-080a-4cec-8fb9-2e257e0d3bcb)

![image](https://github.com/DecloudNodesLab/Projects/assets/23629420/28c10d71-6cfd-4977-86e4-65278fda11ea)

## Step 3 (Usage)

You can use the **v2ray** as a `socks` proxy for your browser or application. And in the role of a VPN connection.

For the browser - set the settings - `socks`, your provider's address and forwarded port from the **LEASES UI CloudMos** tab.

<img src=https://github.com/DecloudNodesLab/Projects/assets/23629420/862dca25-b57c-424f-8a3a-b394aabc558e width=50%>

For example, for Android, there is an [application](https://play.google.com/store/apps/details?id=com.v2ray.ang) **v2ray NG** .
In **v2ray NG** - create a new profile, where specify the provider's address, the `vmess` forwarded port and the `UUID` specified in `config.toml`.
Profile setup example:

<img src=https://github.com/DecloudNodesLab/Projects/assets/23629420/047ef1a7-f219-4b97-9315-b68d9f79e867 width=20%>

More client's application in [v2ray github](https://github.com/v2fly/v2ray-core/releases) and use [v2ray docs](https://www.v2fly.org/en_US/guide/start.html#client) .

**Do you have any questions? Answer on our [Discord](https://discord.gg/rPENzerwZ8)!**
