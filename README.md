## Steps to Verify contracts on Etherscan

### Set etherscan API Key

```
export API_KEY=<etherscan_api_key>
```

### Install node modules

```
npm install
``` 

### Build your contract

You can build your contract with truffle command if not done already.
```
truffle compile
```

Build output file will be <contract>.json

### Update variables in build file
 
- Add/Update compiler information section like below:
```
"compiler": {
    "name": "solc",
    "version": "0.5.0+commit.1d4f565a"
  },
```

- Update correct source path of the contract.
  Example:
  ```
    "sourcePath": "./mosaic-contracts/contracts/gateway/OSTComposer.sol",
  ```

- Add/Update build file with network section.
```
"networks": {
    "3": {
      "address": "0xe322ed07e235a6501bd017ae9ea059b12723c55c",
      "transactionHash": "0xaaae864d3b5b5a81ea7f54d877fc65ddde856577a8646f9a0f011fbb610f463a",
      "links": {}
    }
```
    - address: deployed contract address.
    - transactionHash: Transaction hash when the contract was deployed.
    - links: Library contract addresses.
      Example: {
        "MerklePatriciaProof": "0x168803ca6d5d466ea7005627bfd6eaf0b5b164b0",
        "MessageBus": "0x9c50ad270a2ca1d897326b0880b3f639c3b0acef"
      }
      
    - For verification of library linked contracts, make sure library contract addresses are verified     

### Verify contract

```
npx verify-on-etherscan --network goerli <contract build path> --optimize-runs 200 --output <flattenedFilePath>
```
Example
```
npx verify-on-etherscan --network goerli ./build/contracts/eip20Token.json --optimize-runs 200 --output 200
```

Checkout [more options](https://github.com/gnosis/verify-on-etherscan#as-a-cli-utility).