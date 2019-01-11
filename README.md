# GethLab
Geth Installation Instructions

***How to Install Geth/Ethereum on Mac:***

Step 1: Open Terminal

Go to Launchpad and open terminal. If it is not viewable type it “Terminal” into the search bar and it should appear. Click on it and open terminal

Step 2: Install Homebrew

To install homebrew copy and paste the following command into terminal and click return.
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
Step 3: Install Geth

Once you have installed Homebrew you will need to install Geth. To do so copy and paste the following commands into your terminal one at a time and run them
```
brew update
brew upgrade
brew tap ethereum/ethereum
brew install ethereum
```

Step 4: Once you have reached this step, go to step 2 of the Linux Instructions on the Lab Page. 


***Linux instructions:***

Step 1, Install Geth:
```
apt-get install software-properties-common
add-apt-repository -y ppa:ethereum/ethereum
apt-get update                      
apt-get -y install ethereum
geth --datadir ethdata account new
```

Step 2:

Once geth is created, you'll need to initialize geth using the genesis.json file:
***Do not make any edits to the Genesis.json file***
Download the Genesis file from this repository: https://github.com/natemiller1/GethLab ```wget https://github.com/natemiller1/GethLab/blob/master/genesis.json```

Double check that you have the same genesis.json file as me (and other network particiapnts)

`sha1sum genesis.json` should result in 1b1eda1333dee44c7bd1a1700bf791858a9fd3d1

You'll also need to create a folder to hold the network blockchain data - call it: ethereum_private. Remember where you create the folder, it may be easiest to create it on the desktop/active directory. Once you have the genesis file and new folder, you can initiate the blockchain on your computer. Replace PATH/TO with the folders that lead to your folder/genesis file. The paths may look something like: ~/Desktop/ethereum_private ~/Desktop/genesis.json
```
geth --datadir ~/PATH/TO/ethereum_private init ~/PATH/TO/genesis.json
```

Once initialized, run this code to start the node:
```
geth --datadir=~/.ethereum_private --networkid 1919 --rpc --rpcapi="db,eth,net,web3,personal" --nodiscover console
```


***Windows Instructions***

Get and install Geth from here: https://ethereum.github.io/go-ethereum/downloads/
Install Geth in Program Files\Geth
Inside the Geth folder, put the genesis.json file (from this github: https://github.com/natemiller1/GethLab/blob/master/genesis.json) and create a new folder called ethereumprivate

We'll need to run Geth from the command prompt so hit the windows key and x and click 'powershell(admin)' (We need to run with admin privileges, you may get a warning asking if you're sure you want to do this, hit yes)

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
geth.exe --datadir=ethereumprivate --networkid 1919 --rpc --rpcapi="db,eth,net,web3,personal" --nodiscover console
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

***Installing / Using the Mist wallet***

If you want more functionality you can get Mist, which will make it easier to send Ethereum and create smart contracts. Go to: https://github.com/ethereum/mist/releases/tag/v0.10.0
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
