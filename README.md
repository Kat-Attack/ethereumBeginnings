# ethereumBeginnings
The beginning of my adventures with ethereum.

# What is Ethereum?
Ethereum is a decentralized blockchain platform that allows programming abilities through smart contracts. Gas is needed to make any transaction calls to avoid risk of a repeated attack. 
With Ethereum, apps for all industries could be built on a customized blockchain.

# Installations
Install ethereum and/or geth. Follow this link: https://ethereum.gitbooks.io/frontier-guide/content/installing_linux.html

# Genesis file
We need to create a genesis file to write the very first block in the blockchain. The following is the file's contents:
```javascript
{
    "nonce": "0x0000000000000123",
    "timestamp": "0x0",
    "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "extraData": "0x0",
    "gasLimit": "0x8000000",
    "difficulty": "0x400",
    "mixhash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "coinbase": "0x3333333333333333333333333333333333333333",
    "alloc": {}
}
```
To write the first block, do:
```javascript
geth init genesis.json
```
# Create an account

Now we need to create a unique account (wallet) to make transactions:
```javascript
geth account new
```
You should be prompted to enter a password for your account. 

# Using the node

Create a http-rpc server where you can make web3 calls using:
```javascript
geth --rpc --rpcapi="web3,eth,db,net,personal" --rpcaddr="0.0.0.0" --rpccorsdomain="*" --unlock 0 --networkid 12345 --mine --etherbase 0
```
"--unlock 0" unlocks the first account for you. You must enter your password for that account to continue. To unlock 3 accounts, do "--unlock 0,1,2"

# Connect node to command line
```javascript
node attach
```

To connect to the running server on your machine in order to invoke web3 calls, do
```javascript
geth attach
```

# Clean up

Wipe the existing ethereum directory using:
```javascript
#!/bin/bash

# Kill running geth nodes, if any
instances=`ps aux | grep "geth --rpc" | grep -v grep | wc -l`
if [ $instances != 0 ]; then
	node -e 'require("fkill")("geth")'
fi
```
```javascript
rm -rf ~/.ethereum
```