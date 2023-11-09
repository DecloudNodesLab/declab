# 3proxy on Akash Network
![image](https://user-images.githubusercontent.com/23629420/219872517-2adc32b1-5f64-4d48-9a81-1e2ef6b01a53.png)

**Product documentation:**
| [Site 3Proxy](https://3proxy.ru/) | [GitHub 3Proxy](https://github.com/3proxy) |
|:--:|:--:|
___

# English version

### 3proxy deploy.

Deploy [deploy.yml](https://gitopia.com/DecloudNodesLab/software/tree/master/3proxy/deploy.yml) **3proxy** with **Cloudmos** ([use instructions here](https://docs.declab.pro/guides/cloudmos)).

In this case, a simple proxy server **without authorization** will be deployed, listening on port `8088` for http and port `1080` for a socks proxy. The server configuration is in the executable **shell** [script](https://gitopia.com/DecloudNodesLab/software/tree/master/3proxy/main.sh).
Based on this [script](https://gitopia.com/DecloudNodesLab/software/tree/master/3proxy/main.sh) you can create your own `proxy` with authentication, proxy server type, logging and more.

Details on the configuration on the developer's [website](https://3proxy.ru/download/devel/?l=EN).

![image](https://user-images.githubusercontent.com/23629420/188477186-afd9f6eb-4a10-4a6a-8c21-d2e8ac0f1dc3.png)

After the deployment is complete, specify the `provider.example.com` of the server in your browser settings and **forwarded port** `8088` or `1080` for a socks cnnection.

![image](https://user-images.githubusercontent.com/23629420/188474288-826ba555-ed4f-4462-be65-3d66758d997e.png)

## Thank you for using Akash Network
