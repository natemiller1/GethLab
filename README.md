# GethLab
Geth Installation Instructions


***Linux instructions:***

```
apt-get install software-properties-common
add-apt-repository -y ppa:ethereum/ethereum
apt-get update                      
apt-get -y install ethereum
geth --datadir ethdata account new

```
once geth is created, you'll need to initialize geth using the genesis.json file:
***Do not make any edits to the Genesis.json file***
```
geth --datadir ~/.ethereum_private init ~/PATH/TO/genesis.json
```

Once initialized, run this code to start the node:
```
geth --datadir=~/.ethereum_private --networkid 1919 --nodiscover console
```


***Windows Instructions***

Get and install Geth from here: https://ethereum.github.io/go-ethereum/downloads/
Install Geth in Program Files\Geth
Inside the Geth folder, put the genesis.json file (from this github: https://github.com/natemiller1/GethLab/edit/master/genesis.json) and create a new folder called ethereumprivate

We'll need to run Geth from the command prompt so hit the windows key and x and click 'powershell(admin)' (We need to run with admin privledges, you may get a warning asking if you're sure you want to do this, hit yes)

Next you'll change directories to:
```
cd 'C:\Program Files\Geth'
```
First we'll need to initialize where we will store the blockchain data as well as the genesis block we'll initiate from:
```
geth.exe --datadir=ethereumprivate init genesis.json
```
Once we've initialized, we won't have to do that again, now we can start geth:
```
geth.exe --datadir=ethereumprivate --networkid 1919 --rpc --rpcapi="db,eth,net,web3,personal,web3" --nodiscover console
```

***Once you have geth running (All Users)***

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
***Make sure you get version 0.10.0*** and chose the applicable program for your operating system
Make note of where you installed Mist.

***Starting Mist Windows***, you can do this from either powershell or cmd.exe, just open another instance of it.

```
cd C:\Path\To\Mist
mist.exe --rpc http://localhost:8545
```

***Starting Mist Mac*** open terminal in Mac

```
open -a Mist --args --rpc http://localhost:8545
```
