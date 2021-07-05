# helloeth
Demo app for running demo dapp locally

## setup local node
You can run any number of local nodes. here's a sample of setting up 3 nodes

1. install geth ( on Mac )
brew tap ethereum/ethereum
brew install ethereum
 ( For more environment setup checkout https://geth.ethereum.org )

2. Genesis Block - This is very first block for your local node. Each Node in the network will be initialized with the same genesis block.

```json
{
    "config": {
        "chainId": 15,				[//]: # ( get the list of mainnet / testnet chainid from https://chainid.network/chains.json.)
        "homesteadBlock": 0,
        "eip150Block": 0,
        "eip155Block": 0,
        "eip158Block": 0
    },
    "difficulty": "400000",	
    "gasLimit": "2100000",
    "alloc": {
        "0xA2c9aF63ebdE9c217245877967892332772EfcC7": { "balance": "1000000000000000000" },  //Balance in wei 
        "0x09E508723110e4FEB57A7Dcef284687428c04aC0": { "balance": "1000000000000000000" }   // Balance in wei
    }
}
```

3. Local Block Nodes - Running locally makes this blockchain private ( only you can deploy / test / create blocks ). This is a perfect candidate for local development and testing. Navigate to your blockchain directory 

```json
mkdir node01 node02 node03
``` 
4. Local Accounts - This will create 2 ethereum accounts as shown in the genesis file. Write down the address and memorize the password.

```json
geth --datadir "PATH_TO_NODE01" account new	
```

5. Initialize - Now you can run the 'init' to kickstart the local blockchain network.

```json
geth --datadir "PATH_TO_NODE01" init "PATH_TO/genesis.json"
```
Followed by starting each node with 

```json
geth --identity "node01" --http --http.port  "5000" --http.corsdomain  "*" --datadir "/PATH_TO_NODE01/node01" --port "40303" --nodiscover --http.api  "db,eth,net,web3,personal,miner,admin" --networkid 1900 --nat "any" --allow-insecure-unlock  --ethstats node01:s3cr3t@localhost:3000

geth --identity "node02" --http --http.port  "6000" --http.corsdomain  "*" --datadir "/PATH_TO_NODE02/node02" --port "50303" --nodiscover --http.api  "db,eth,net,web3,personal,miner,admin" --networkid 1900 --nat "any" --allow-insecure-unlock --ethstats node01:s3cr3t@localhost:3000

geth --identity "node03" --http --http.port  "7000" --http.corsdomain  "*" --datadir "PATH_TO_NODE03/node03" --port "60303" --nodiscover --http.api  "db,eth,net,web3,personal,miner,admin" --networkid 1900 --nat "any" --allow-insecure-unlock --ethstats node01:s3cr3t@localhost:3000

```

6. Now you can connect to local nodes with geth. For whole set of commands, visit https://geth.ethereum.org/docs/interface/command-line-options

```json
geth attach http://127.0.0.1:5000 // Attaching to Node01

eth.accounts

eth.getBalance(eth.accounts[0])
```

7. Smart Contract  - A simple dApp that transfer funds. Using solidity. Checkout https://docs.soliditylang.org/ for syntax
 - compile the code with 'solc tranfer_fund', Which will generate the abi.
 - connect to local blockchain using etherjs / web3 and deploy the abi. ( you can use ganache as well.)

8. Checkout HardHat ( https://hardhat.org/getting-started/#connecting-a-wallet-or-dapp-to-hardhat-network ) or Truffle( https://www.trufflesuite.com ) for deploying interacting with smart contract.
