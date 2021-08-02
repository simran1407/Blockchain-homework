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

- Now we export genesis configurations. This will fail to create two of the files, but we only need simnet.json.

<img width="1045" alt="sc5" src="https://user-images.githubusercontent.com/78338890/127789849-e9e594a2-0b31-4469-9493-efee937307bb.png">


- With the genesis block creation completed, we will now initialize the nodes with the genesis' json file.

- Using geth, we initialize each node with the new simnet.json.

./geth --datadir node1 init simnet.json
./geth --datadir node2 init simnet.json

<img width="1439" alt="sc3" src="https://user-images.githubusercontent.com/78338890/127789777-491c1545-51a0-4c41-9e8b-92a4e672e40f.png">

- Now the nodes can be used to begin mining blocks.

- Run the nodes in separate terminal windows with the commands:

./geth --datadir node1 --unlock "0xd5b9fa27550306b8a662Eb89a98020A3cCecDc46" --mine --rpc --allow-insecure-unlock
./geth --datadir node2 --port 30304 --bootnodes "enode://22ff1742d774b7d29d1215c25b7e39469a9ac923ee95e1e63fb2ddf0c13e7267df4933aa9692fde3ee2805078b64408ce1fcf1e1022ddda5e87b930a4dce6063@127.0.0.1:30303"

<img width="1440" alt="sc4" src="https://user-images.githubusercontent.com/78338890/127789803-128265b0-05e6-44e3-9f2c-3f2edce4b651.png">

<img width="1424" alt="sc12" src="https://user-images.githubusercontent.com/78338890/127789871-0bd4c4f8-f521-48a2-9e5b-68bb3bd4502c.png">

- Our private PoA blockchain is now running!

- With both nodes up and running, we will add the blockchain  to MyCrypto for testing.

- So we open the MyCrypto app, then click Change Network at the bottom left and click "Add Custom Node", then add the custom network information that we have set in the genesis.
      - Type ETH in the Currency box
      - In the Chain ID box, we type the chain id we generated - 999
      - In the URL box type: http://127.0.0.1:8545.  This points to the default RPC port on our local machine.
      - Then we finally, click Save & Use Custom Node.

<img width="1389" alt="sc6" src="https://user-images.githubusercontent.com/78338890/127790367-1c4f5f3e-ce98-4727-b92d-4fb6318851e2.png">

- After connecting to the custom network in MyCrypto, we test by sending money between accounts.
 
 - So we select the View & Send option from the left menu pane, then click Keystore file. On the next screen, we click Select Wallet File, then navigate to the keystore directory inside our Node1 directory, select the file located there, provide our password when prompted and then click Unlock and this will open our account wallet inside MyCrypto.

<img width="1360" alt="sc7" src="https://user-images.githubusercontent.com/78338890/127790508-8217db09-1073-47ce-9ed1-f1d488633745.png">


We're filthy rich! :)
This is the balance that was pre-funded for this account in the genesis configuration; however, these millions of ETH tokens are just for our testing purposes.

-Now in the To Address box, we type the account address from Node2, then fill in the amount of 250 ETH:
<img width="1367" alt="sc8" src="https://user-images.githubusercontent.com/78338890/127790624-ac8206e3-a756-4d4a-bbb2-18e6d8fb4196.png">

- Now we confirm the transaction by clicking "Send Transaction", and the "Send" button in the pop-up window:
<img width="1266" alt="sc9" src="https://user-images.githubusercontent.com/78338890/127790669-4154d551-9890-4688-b17a-dedea894ad16.png">

- We then click the Check TX Status when the green message pops up and confirm the logout.
<img width="1340" alt="sc10" src="https://user-images.githubusercontent.com/78338890/127790722-1837b669-736d-4a5d-9403-c80693fb019e.png">

Now we can click the Check TX Status button to update the status. And it may take some time to go from. pending to successful.

<img width="1353" alt="sc11" src="https://user-images.githubusercontent.com/78338890/127790768-55c1a232-27ea-44dd-bedc-3508116c9ea6.png">



