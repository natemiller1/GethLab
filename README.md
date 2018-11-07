# GethLab

***Linux instructions:***
Install Geth using these instructions:

```
apt-get install software-properties-common
add-apt-repository -y ppa:ethereum/ethereum
apt-get update                      
apt-get -y install ethereum
geth --datadir ethdata account new

```

***Windows Instructions***
Get and install Geth from here: https://ethereum.github.io/go-ethereum/downloads/


once geth is created, you'll need to initialize geth using the genesis.json file:
***Do not make any edits to the Genesis.json file***
```
geth --datadir ~/.ethereum_private init ~/PATH/TO/genesis.json
```

Once initialized, run this code to start the node:
```
geth --datadir=~/.ethereum_private --networkid 1919 --nodiscover console
```


Creating an account. You'll be asked to provide a passphrase.
```
personal.newAccount()
```
Defining your initial/primary account as coinbase:
```
miner.setEtherbase(eth.accounts[0])
```
Verify coinbase:
```
eth.coinbase
```
Go to the google sheet and copy the admin.addPeer code from the enode column in its entirety and enter in the console

check that the nodes are connected:

```
admin.peers
```

After that's done you can start and stop the mining process by using the below code. The first time you start mining, you will need to install DAG (a specific dataset related to proof of work), this will take a minute or so, then mining will commence.
```
miner.start(1)
miner.stop()
```
If you want more functionality you can get Mist, which will make it easier to send Ethereum and create smart contracts, go to: https://github.com/ethereum/mist/releases/tag/v0.10.0
Make sure you get version 0.10.0 and chose the applicable program for your operating system
Make note of where you installed Mist.

Starting Mist Windows

```
cd C:\Path\To\Mist
mist.exe --rpc http://localhost:8545
```

