<p align="center"><img src="https://user-images.githubusercontent.com/23629420/219872517-2adc32b1-5f64-4d48-9a81-1e2ef6b01a53.png" </p>
  
> An overview and guide to using the console Akash custom web user interface.

<div align="center">
  
|[Akash Network](https://akash.network/)|[Discord Akash](https://discord.akash.network/)|[Twitter Akash](https://twitter.com/akashnet_)|
|:--:|:--:|:--:|
|[Decloud Nodes Lab](https://declab.pro)|[Discord Decloud Nodes Lab](https://discord.gg/eDKdvjfUAS)|[Twitter Decloud Nodes Lab](https://twitter.com/NodesLab)|

</div>

# Account connection and preparation for work.

Login to [web UI console Akash](https://console.akash.network) using the Keplr app:

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221588325-7ef4f756-4706-4106-8a3a-839034782469.gif"</p>

  
## Create certificate
  
  > Top up your AKT account. Please note that ***0.5 AKT*** are blocked on the account with each deployment + a small amount of AKT is required to pay for gas. Thus, for the test it is enough to replenish the account with ***1 AKT***. The AKT token can be purchased on the ```Gate```, ```AsendeX```, ```Osmosis``` exchanges.


After the AKT account is replenished, it is necessary to request and install a certificate from the blockchain, for this:
  
1. At the top right, click ***CREATE CERTIFICATE***.
2. Select the transaction fee and confirm the transaction.

The certificate has been created, you can see it in the upper right corner of the window.

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221591238-e1858e2f-eb8f-4ff1-a01b-269dbb91e1af.gif"</p>

Preparation is complete, now let's do a test forking.

___

# Test deployment

***Console Akash*** has ready-made ***manifest files (deploy.yml)***, they are located in the ```Templates``` tab, check out the offer of ready-made solutions:

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221591869-b37798b8-76d6-476f-8c3d-ec8be35683db.png"</p>

Let's deploy the well-known game ***Super Mario***, to do this, select the appropriate section ***Games*** in ```Templeates``` and click on ```Super Mario```:

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221592345-5eb3f69a-c391-40e1-8d3b-203d7a87069d.png"</p>

Click ***Deploy***:

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221592527-cc96d385-e682-4ad8-bd47-e2308f9116df.png"</p>

***Console Akash*** quickly checks for the presence of a certificate and ***0.5 AKT*** on the balance sheet, and opens the completed ***manifest window (deploy.yml)***, let's dwell on the contents of the manifest:

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221593433-2e94845d-3db2-4adf-acf8-672570b6340c.png"</p>
  
Here pay attention to:

Section ```services``` (lines 4-11). Line 6 specifies the image in ***Docker hub*** from which the container will be deployed, in our case it is ```pengbai/docker-supermario```. The ***expose*** subsection is responsible for opening and forwarding ports. In our case, port 8080 is represented as 80 external.

Section ```profiles``` (lines 13-22) here in the subsection ```resources``` we indicate the rented characteristics of the equipment for our container with the game ***Super Mario***. In our case, this is ```1 cpu, 512 MB of RAM and 512 MB of hard disk```. Enter a name for the deployment at the top and click ***CREATE DEPLOYMENT***.
  
<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221593892-f1385fd5-5d68-45e3-b74a-c0bec7a9e6bc.png"</p>

We deposit ***0.5 AKT*** from our account, press ```DEPOSIT```:

Set the transaction fee and confirm it. At this stage, we have sent a capacity request to the network for our game container. We just have to wait for a response from providers with their offers and prices. ***Please note that 0.5 AKT have been deposited from your account***.

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221594641-9f02b27b-04b6-4459-9108-ebb852b40434.png"</p>

Select a provider and press ```ACCEPT BID```, once again set the commission for the transaction and confirm it. We are waiting for the container to be deployed. Once the container is deployed, go to the ```LEASES``` tab.

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221595596-3e2ecd06-2b3a-462b-97db-c8e3466f3c41.png"</p>

Information about your provider, rental cost, as well as an individual link to your deployment are available here. Click on it.
  
<p align="center"><img src="https://user-images.githubusercontent.com/23629420/179998220-473b42ec-144f-4bff-b640-801fc727983b.png"</p>

Great! It looks like you deployed the game to Akash Network! But you need something more than a game? Then go to the section describing the functionality of ***console Akash*** =)
  
___
  
# Contents of the deployment window

The ```Dashboard``` tab displays your active forks, go to it.

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221596081-3ec6f4eb-2987-4aff-b0dd-33fe2ba045f6.png"</p>

As we learned earlier, the ```LEASES``` tab contains general information about the deployment - provider, resources, forwarded ports and links.

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221596340-5d4a87b7-3d53-47d3-a00e-d50fadfbaf5a.png"</p>

There are 2 more subsections in the ```LOGS``` tab, this is the ```LOGS``` subsection - logs ***INSIDE*** of the container are displayed here (by clicking the ```DOWNLOADS LOGS``` button, you can download them to file):

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221596683-75800c6a-1a59-4753-84ab-45c7ac0463fa.png"</p>

and the ```EVENTS``` subsection - here you can see ***k8s*** logs, the process of downloading and starting your image:

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221596900-39597059-c8f2-4d5a-a1af-b3955c04f7ce.png"</p>

On the ```SHELL``` tab, you can use some ***NOT interactive*** commands inside the container
  
<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221597223-d678a85b-7091-4cc2-bfa1-2d3e4d24a7e5.png"</p>

The ```UPDATE``` tab contains the current ***manifest (deploy.yml)***, here you can add variables or change the image version, in which case the container will be restarted. ***(IMPORTANT! Resources cannot be changed! To do this, close deployment and redeploy!).***
  
<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221597762-983bbe87-d4a9-41fe-828c-a059a7346736.png"</p>

The ```RAW DATA``` tab contains ```JSON``` information from the ```AKASH``` blockchain
  
<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221598012-a444a5c6-0a98-4d35-9ce8-0cf63579eb28.png"</p>

___

# Close deployment

To close the deployment, you need to click ```CLOSE``` in the context menu and confirm the transaction


<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221598510-9450f1ae-5b2c-4037-bb79-cc24d0d03a36.png"</p>

After the deployment is closed, the balance of ***AKT*** will be returned to your main account.
  
___

  
# Overview of console Akash functionality.
  
***Dashboard*** - Shows your current account details(1), current online lease status(2) and your active deployments(3).

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221599302-10794063-abb5-4303-9f59-f501a8561740.png"</p>

***Deployments*** - all fanouts ever created on your address, including those that are not active.

   <p align="center"><img src="https://user-images.githubusercontent.com/23629420/221599517-615a7796-bae8-4cba-8c96-acae9de506a8.png"</p>

***Templates*** - ready-made solutions for deployments, games, database, website builders, miner, etc..

   <p align="center"><img src="https://user-images.githubusercontent.com/23629420/221599709-f8969486-a26d-408c-9aac-671dfcff9b32.png"</p>
  
***Provider*** - a list of existing providers in the Akash Network marketplace with their equipment parameters.

  <p align="center"><img src="https://user-images.githubusercontent.com/23629420/221599849-e1cf4f85-d25a-418e-a4b5-077634d2ebf0.png"</p>

***Settings*** - RPC node settings for the application (1). Quick switching is also available in the field at the top of the window (2).

<p align="center"><img src="https://user-images.githubusercontent.com/23629420/221600341-ecb778bd-857e-420e-b13d-b7ff4f22e8ec.png"</p>
  
___
