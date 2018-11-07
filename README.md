# GethLab

Install Geth using these instructions:

```
apt-get install software-properties-common
add-apt-repository -y ppa:ethereum/ethereum
apt-get update                      
apt-get -y install ethereum
geth --datadir ethdata account new

```

once geth is created, you'll need to initialize geth using the genesis.json file:

```
geth --datadir ~/.ethereum_private init ~/PATH/TO/genesis.json
```

Once initialized, run this code to start the node:
```
geth --datadir= ~/.ethereum_private --networkid 1919 --nodiscover console
```
