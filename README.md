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

```

Step 2:

Once geth is created, you'll need to initialize geth using the genesis.json file:
***Do not make any edits to the Genesis.json file***
Download the Genesis file from this repository: https://github.com/natemiller1/GethLab ```wget https://raw.githubusercontent.com/natemiller1/GethLab/master/genesis.json```

Double check that you have the same genesis.json file as me (and other network particiapnts, capitalization doesn't matter)

`sha1sum genesis.json` should result in 44030c0d27885669eea187eeccf8be0e7148c183

`sha256sum genesis.json` should result in b5836675e0db566b249cf3c293938bb6f410a4e8fbc74d43b4fa3d6f86e78901

You'll also need to create a folder to hold the network blockchain data - call it: ethdata. Remember where you create the folder, it may be easiest to create it on the desktop/active directory. Once you have the genesis file and new folder, you can initiate the blockchain on your computer. Replace PATH/TO with the folders that lead to your folder/genesis file. The paths may look something like: ~/Desktop/ethdata ~/Desktop/genesis.json
```
geth --datadir ~/PATH/TO/ethdata init ~/PATH/TO/genesis.json
```

Once initialized, run this code to start the node:
```
geth --datadir ~/PATH/TO/ethdata --networkid 1919 --rpc.allow-unprotected-txs --http.api eth,net,web3,personal --http --nodiscover console
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
geth.exe --datadir=ethdata init genesis.json
```
Once we've initialized, we won't have to do that again, now we can start geth:
```
geth.exe --datadir ~/PATH/TO/ethdata --networkid 1919 --rpc.allow-unprotected-txs --http.api=“db,eth,net,web3,personal” --nodiscover console
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

https://docs.google.com/spreadsheets/d/17ed-1gr6TlUMxhpu3OBVUEU_3aRr1RTm2roUwPoZ9E4/edit#gid=0

check that the nodes are connected, there should be a list of the node's attributes:

```
admin.peers
```

***Occassionally, I'll run into issues connecting peers, if you run the admin.addPeer code and receive 'true' but admin.peers results in [], exit geth and reinitialize your datadir (add a 1 to the directory): ```geth --datadir ~/PATH/TO/ethdata1 init ~/PATH/TO/genesis.json``` then restart geth with the new datadir ```geth --datadir ~/ethdata --networkid 1919 --rpc.allow-unprotected-txs --http.api=“db,eth,net,web3,personal” --nodiscover console```***

After that's done you can start and stop the mining process by using the below code. The first time you start mining, you will need to install DAG (a specific dataset related to proof of work), this will take a minute or so, then mining will commence.
```
miner.start(1) #the number indicates how many of your CPU cores are being used for mining.
miner.stop()
```

You can also peer with each other, by default your geth instance will be able to TCP peer over port 30303. You can change this when starting geth by adding the tag ```--port 3020``` (or whatever port you want, avoid anything under 1025). Once geth is running you can type ```admin.nodeInfo``` which will display your enode address. To add a peer, ```admin.addPeer("enode://xxxxxxx@ipaddress:port?discport=0")```

***Installing / Using the Mist wallet***

If you want more functionality you can get Mist, which will make it easier to send Ethereum and create smart contracts. Go to:

https://github.com/ethereum/mist/releases/tag/v0.10.0

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

***Using MetaMask*** MetaMask is a simple browser extension that serves as a wallet.

Head to metamask.io and install the browser extension. Once your account is created, you'll need to back up your wallet with a seed code (we aren't using real ethereum so this step isn't that important, but if you decide to use MetaMask as an actual wallet, please do not store your seed phrase on your computer).

After your account is created, there is a button in the top right that should say Main Ethereum Network - if you click on that and select localhost:8545, it should connect to your Geth instance.


