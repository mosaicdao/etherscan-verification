## Steps to Verify contracts on Etherscan

### Set etherscan API Key

```
export API_KEY=<etherscan_api_key
```

### Install node modules

```
npm install
``` 

### Build your contract

You can build your contract with truffle command
```
truffle compile
```

Build output file will be <contract>.json

### Set variables in build file

With truffle compile below fields are already populated in JSON file. Make sure they are updated if not present.
 
- Add compiler information section like below:
```
"compiler": {
    "name": "solc",
    "version": "0.5.0+commit.1d4f565a.Emscripten.clang"
  },
```

- Update correct source path of the contract.
  Example:
  ```
    "sourcePath": "./mosaic-contracts/contracts/gateway/OSTComposer.sol",
  ```

- Update build file with network section.
```
"networks": {
    "3": {
      "address": "0xe322ed07e235a6501bd017ae9ea059b12723c55c",
      "transactionHash": "0xaaae864d3b5b5a81ea7f54d877fc65ddde856577a8646f9a0f011fbb610f463a",
      "links": {}
    }
```
address: deployed contract address.
transactionHash: Transaction hash when the contract was deployed.
links: Library contract addresses. 

### Verify contract

```
npx verify-on-etherscan --network goerli <contract build path>
```
Example
```
npx verify-on-etherscan --network goerli ./build/contracts/eip20Token.json
```

Checkout [more options](https://github.com/gnosis/verify-on-etherscan#as-a-cli-utility).