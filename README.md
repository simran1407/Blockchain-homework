# Running a Proof of Authority Blockchain

The Proof of Authority (PoA) algorithm is typically used for private blockchain networks as it requires pre-approval of, or voting in of, the account addresses that can approve transactions (seal blocks). Because the accounts must be approved, we will generate two new nodes with new account addresses that will serve as our pre-approved sealer addresses.

- First we will create accounts for two nodes for the network with a separate datadir for each using geth.

./geth --datadir node1 account new
./geth --datadir node2 account new



<img width="1436" alt="sc1" src="https://user-images.githubusercontent.com/78338890/127782316-a372be1a-b966-4f30-bff9-fecc9057228f.png">


- Next, we generated our genesis block.

- Ran puppeth, named our network as "simnet" in this case, and selected the options to configure a new genesis block.

- Now we choose the Clique (Proof of Authority) consensus algorithm.

- Now paste both account addresses from the first step one at a time into the list of accounts to seal and paste them again in the list of accounts to pre-fund. There are no block rewards in PoA, so we'll need to pre-fund.

- We choose "no" for pre-funding the pre-compiled accounts (0x1 .. 0xff) with wei. This keeps the genesis cleaner.

- Then we specify our chain/network ID = 999 (in this case).

<img width="1439" alt="sc2" src="https://user-images.githubusercontent.com/78338890/127783088-bd9d6926-6d47-4006-ac9c-3fdedadaa907.png">


- Then we complete the rest of the prompts, and when we are back at the main menu, we choose the "Manage existing genesis" option.

- Now we export genesis configurations. This will fail to create two of the files, but you only need networkname.json.




With the genesis block creation completed, we will now initialize the nodes with the genesis' json file.

Using geth, initialize each node with the new simnet.json.

./geth --datadir node1 init simnet.json
./geth --datadir node2 init simnet.json


Now the nodes can be used to begin mining blocks.

Run the nodes in separate terminal windows with the commands:

./geth --datadir node1 --unlock "0xd5b9fa27550306b8a662Eb89a98020A3cCecDc46" --mine --rpc --allow-insecure-unlock
./geth --datadir node2 --port 30304 --bootnodes "enode://22ff1742d774b7d29d1215c25b7e39469a9ac923ee95e1e63fb2ddf0c13e7267df4933aa9692fde3ee2805078b64408ce1fcf1e1022ddda5e87b930a4dce6063@127.0.0.1:30303"


Your private PoA blockchain should now be running!


With both nodes up and running, the blockchain can be added to MyCrypto for testing.

Open the MyCrypto app, then click Change Network at the bottom left:
