Clone three repos to these folders:

```
C:\> git clone https://github.com/BigBangInfinity/ballot_NFT_shared-backend-my-api
C:\> git clone https://github.com/BigBangInfinity/ballot_NFT_shared-ballotcontract
C:\> git clone https://github.com/BigBangInfinity/ballot_NFT_shared-scaffold-eth-2
```

npm/yarn install in these folders

use npm for ballotcontract and yarn for others because this is what I used for these folders.

```
C:\ballot_NFT_shared-backend-my-api> yarn install
C:\ballot_NFT_shared-ballotcontract> npm install
C:\ballot_NFT_shared-scaffold-eth-2> yarn install
```

Compile contract
```
C:\ballot_NFT_shared-ballotcontract>npx hardhat compile 
```

Deploy token contract
```
C:\ballot_NFT_shared-ballotcontract>npx ts-node .\scripts\deployMyNFT.ts
```

token contract deployed at 0xC895Edd7C0D122e02f13c84C401AEc00e1d999F8

Verify on etherscan:

```
C:\ballot_NFT_shared-ballotcontract>npx hardhat verify --network sepolia 0xC895Edd7C0D122e02f13c84C401AEc00e1d999F8
```



In  C:\ballot_shared-ballotcontract\scripts\deployTokenizedBallot.ts,
update token address in ballot.

const myTokenAddress = "0xC895Edd7C0D122e02f13c84C401AEc00e1d999F8";


Deploy tokenized ballot
```
C:\ballot_shared-ballotcontract>npx ts-node .\scripts\deployTokenizedBallot.ts
```
Ballot contract deployed on 0xff07015a33F24C5885807802D0065BE38955DeA9

To verify with hardhat, we have to pass the constructor arguments into the verifier, and the proposal names have to be converted to bytes.
To get the bytes representation, run 
```
C:\ballot_shared-ballotcontract>npx ts-node .\scripts\encodeStrings.ts 
```
The strings ["Bored Ape Yacht Club", "CryptoPunks", "Pudgy Penguins"] are converted to 
```
[
  '0x426f7265642041706520596163687420436c7562000000000000000000000000',
  '0x43727970746f50756e6b73000000000000000000000000000000000000000000',
  '0x50756467792050656e6775696e73000000000000000000000000000000000000'
]
```
Create arguments.json file which contains the constructir arguments which are needed for Etherscan verification:
```
[
    [
        "0x426f7265642041706520596163687420436c7562000000000000000000000000",
        "0x43727970746f50756e6b73000000000000000000000000000000000000000000",
        "0x50756467792050656e6775696e73000000000000000000000000000000000000"
    ],
    "0xff07015a33F24C5885807802D0065BE38955DeA9"
]
```

verify on etherscan:

```
C:\ballot_shared-ballotcontract>npx hardhat verify --network sepolia --constructor-args arguments.json 0xff07015a33F24C5885807802D0065BE38955DeA9 
```



in C:\ballot_NFT_shared-backend-my-api\.env, update token address:
TOKEN_ADDRESS = "0xC895Edd7C0D122e02f13c84C401AEc00e1d999F8"
BALLOT_ADDRESS = "0xff07015a33F24C5885807802D0065BE38955DeA9"

in C:\ballot_NFT_shared-scaffold-eth-2\packages\nextjs\.env.local, update token address (environment variable has to start with NEXT_PUBLIC):
NEXT_PUBLIC_TOKEN_ADDRESS = "0xC895Edd7C0D122e02f13c84C401AEc00e1d999F8"
NEXT_PUBLIC_BALLOT_ADDRESS =  "0xff07015a33F24C5885807802D0065BE38955DeA9

```
C:\ballot_NFT_shared-backend-my-api>yarn run start:dev
```      

Launches Swagger API on 
http://localhost:3001/route

```
C:\ballot_NFT_shared-scaffold-eth-2>yarn start
```

Launches Scaffold ETH on 
http://localhost:3000

Request NFT tokens on the frontend

![image](https://github.com/BigBangInfinity/ballot_NFT_shared-main/assets/37957341/d91f2fb6-fba9-42a3-b9c5-f2d6c2b143c7)



delegate vote to yourself or to someone else.

![image](https://github.com/BigBangInfinity/ballot_NFT_shared-main/assets/37957341/670e87db-e29b-46e0-aba1-88af1b135370)



Vote for proposals (index numbers 0, 1 or 2), 
put in number of votes,

![image](https://github.com/BigBangInfinity/ballot_NFT_shared-main/assets/37957341/e9af84a4-5a89-45e1-8796-b3726514f6dd)



and then read results.


![image](https://github.com/BigBangInfinity/ballot_NFT_shared-main/assets/37957341/e55e1284-109c-48c0-871c-fe731e962e0f)
