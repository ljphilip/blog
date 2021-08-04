---
title: "Minting NFTs on Algo using Command Line Interface- A step by step tutorial"
date: 2021-07-30T16:51:00+05:30
# weight: 1
# aliases: ["/first"]
tags: ["NFT", "Algorand", "blockchain"]
author: "LJP"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "A step by step guide on minting NFTs on Algorand blockchain using Goal CLI"
#canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
#editPost:
#    URL: "https://github.com/<path_to_repo>/content"
#    Text: "Suggest Changes" # edit text
#    appendFilePath: true # to append file path to Edit link
---
### The story

I have been interacting with an artist (MJL) over reddit for a while and with a view to supporting the Ravencoin (RVN) community, MJL started creating digital arts as NFTs on RVN and I, buying them using RVNs- all of them were great works! (but that's a story for another day I guess). I have been more bullish on Algorand blockchain though and I had read Algo supports minting of NFTs. I proposed creation of NFTs on Algo and MJL was open to the idea. Thing is both of us did not know how to create an NFT on Algo and I offered to learn to create an NFT on Algo (I know, the confidence right? :D) and MJL offered a discount in return. Below is the steps I followed- writing it down so I don't forget and so that it acts like a tutorial of sorts for a non-tech person (like an artist like MJL) to create an NFT without having to rely on a third party developer\website.

### Reference Article

The tutorial I followed to create the NFT was this: [https://developer.algorand.org/tutorials/create-and-manage-non-fungible-asa-command-line-using-goal/#4-asa-property-unitname](https://developer.algorand.org/tutorials/create-and-manage-non-fungible-asa-command-line-using-goal/#4-asa-property-unitname)

This is a very good tutorial- so you can just head to that tutorial; and come back here only if you are stuck in any of the steps. The two points the above tutorial do not cover are how to create your account\wallet and how to transfer the assets you create. 

Below steps are for creating NFT on a mac.

### Pre-requisites

- You need to install Algo 'node' and with it you get the Goal Command Line Interface. (Accordingly, all your interactions for NFT creation will be through the Mac terminal).
- You need to create your algo account and wallet

### Installing Node and Goal CLI

- Head to this link and follow the steps : [https://developer.algorand.org/docs/run-a-node/setup/install/](https://developer.algorand.org/docs/run-a-node/setup/install/) OR
- Run the following commands in your mac terminal (one after the other):

    ```python
    mkdir ~/node
    cd ~/node
    curl https://raw.githubusercontent.com/algorand/go-algorand-doc/master/downloads/installers/update.sh -O
    chmod 544 update.sh
    ./update.sh -i -c stable -p ~/node -d ~/node/data -n

    export ALGORAND_DATA="$HOME/node/data"
    export PATH="$HOME/node:$PATH"
    ```

When you type 'goal' on terminal and if you get a command not found error, type the last two commands above. It guides the terminal to the path where goal is installed.

- to check that you have successfully installed goal, type `goal` and enter; you will get a description of what goal is and the commands it supports
- The above link also has steps on how to get your node up to date with the blockchain data. You could follow those as well. I am not entirely sure if this is a mandatory step to create the asset. I followed it just to be sure. First visit the link and copy the text from the result page: [https://algorand-catchpoints.s3.us-east-2.amazonaws.com/channel/mainnet/latest.catchpoint](https://algorand-catchpoints.s3.us-east-2.amazonaws.com/channel/mainnet/latest.catchpoint) and Then run the commands mentioned below. In `goal node catchup` command below, instead of the text below starting with 44200..., paste the text you get from the link mentioned in this point:

```python
goal node start
goal node catchup 4420000#Q7T2RRTDIRTYESIXKAAFJYFQWG4A3WRA3JIUZVCJ3F4AQ2G2HZRA
```

- you can type `goal node status` command to see if your node is fully synchronised with the blockchain; you can verify this by checking in the result if Sync Time is 0.0s

### Creating Algo Account and Wallet

- again, you can head to this link for a more detailed set of instructions: [https://developer.algorand.org/docs/features/accounts/create/#:~:text=token%3A [token]-,Create a wallet and generate an account,wallet handle%2C generate an account](https://developer.algorand.org/docs/features/accounts/create/#:~:text=token%3A%20%5Btoken%5D-,Create%20a%20wallet%20and%20generate%20an%20account,wallet%20handle%2C%20generate%20an%20account); or type the commands below, one after the other:

```python
goal kmd start -t 3600

goal wallet new [walletname]
goal account new
```

For '[walletname]', substitute it with a name you want to have for your wallet

remember the address created upon the `goal account new` command.

### Creating the Asset\NFT

Use the following command

```python
goal asset create --asseturl "ipfs://QmNRMPLbphnnCysgo3B53faAwXH7M6XJwxZNeMDHGSed4i"  --assetmetadatab64 55b83f286cef95fbe5c71dbd51bc5c38 --creator L4ZO6WFU65X2C2RGZWD6MPL5R2DD2X5 --decimals 0 --name "Sight Seer2" --noteb64 "aHR0cHM6Ly9pcGZzLmlvL2lwZnMvUW1OUk1QTGJwaG5uQ3lzZ28zQjUzZmFBd1hIN002WEp3eFpOZU1ESEdTZWQ0aT9maWxlbmFtZT1RbU5STVBMYnBobm5DeXNnbzNCNTNmYUF3WEg3TTZYSnd4Wk5lTURIR1NlZDRp" --total 1 --unitname "MJLSSRTS" --datadir "$HOME/node/data" --wallet "ljnftwallet"
```

Essentially, `goal asset create` is the basic command to create a new asset and the details of the other parameters are as follows:

—asseturl: the url/link providing more details about the asset. In case of NFT, the art file could be uploaded to IPFS system (check out more here: [https://ipfs.io](https://ipfs.io/)). IPFS is also a decentralised system and each file is provided a unique CIN. You can download IPFS desktop and upload your file and get a CIN and URL for the file.

—assetmetadatab64: you can provide base-64 encoded 32-byte meta information here. For example you can separately send a certificate of authenticity signed by you separately and if you use a free encoder to create a hash of the file, you can provide the hash here; so that it is easy to prove that the certificate is associated with this particular NFT. Since it only supports 32 bytes (roughly 32 characters), you can use MD5 hash. (There are free online sites which allow you to generate hash of a file.

—creator: here you mention your account address

—decimal: Since NFT are non fungible, you would want to keep the decimal to 0

—name: Any name you want to give to the token

—note64: here you can again provide URL-base64 encoded; alternatively, you can use —note to provide any additional text description you want to be associated with the token

—unitname: has a limit of 8bytes; typically, capitalised abbreviations

—datadir: location of your node data

—wallet: your wallet name

## configuring the asset\NFT

Use the following command:

```python
goal asset config --asset MJLSSRTS --creator LEE --manager L4E --new-clawback "" --new-freezer "" --note "test asset"  --datadir "$HOME/node/data" --wallet "ljnftwallet"
```

You need to use the above command to configure the asset you just created because if you use Goal to create the asset, it will have clawback and freezer addresses by default. Clawback address has the power to transfer the asset from any owner's account to another account and freeze address has the power to freeze further trading of the assets. You do not want these features if you are planning to sell your NFT to a third party buyer. Thus you configure and mention `—new-clawback` and `—new-freezer` accounts as blank ""

note that creating and configuring takes 0.001 Algo transaction fees each.

### Transferring the Asset

To transfer the asset to an address, use the following command:

```python
goal asset send --amount 1  --assetid 285558186 --to WWLABAFWLQ
```

where

--to is the wallet address
