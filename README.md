# truffle-hdwallet-provider
HD Wallet-enabled Web3 provider. Use it to sign transactions for addresses derived from a 1-24 word mnemonic.

## Install

```
$ npm install truffle-safe-hdwallet-provider
```

## General Usage

You can use this provider wherever a Web3 provider is needed, not just in Truffle. For Truffle-specific usage, see next section.

### HDWalletProvider Signature
The following is the function signature of the HDWalletProvider fuction:
```javascript
function HDWalletProvider(mnemonic, provider_url, address_index=0, num_addresses=1, password='')
```

###Usage

```javascript
var HDWalletProvider = require("truffle-safe-hdwallet-provider");
var mnemonic = "opinion destroy betray ..."; // 12 word mnemonic
var provider = new HDWalletProvider(mnemonic, "http://localhost:8545");

// Or, alternatively pass in a zero-based address index.
var provider = new HDWalletProvider(mnemonic, "http://localhost:8545", 5);

// Or, alternatively pass in also the ammount of addresses to list.
var provider = new HDWalletProvider(mnemonic, "http://localhost:8545", 5, 1);

// Or, alternatively pass in also the password that encoded the mnemonic phrase.
var provider = new HDWalletProvider(mnemonic, "http://localhost:8545", 5, 1, 'a password');

```

By default, the `HDWalletProvider` will use the address of the first address that's generated from the mnemonic. If you pass in a specific index, it'll use that address instead. Currently, the `HDWalletProvider` manages only one address at a time, but it can be easily upgraded to manage (i.e., "unlock") multiple addresses.

Parameters:

- `mnemonic`: `string`. 1-24 word mnemonic which addresses are created from. (checksum not currently enforced)
- `provider_uri`: `string`. URI of Ethereum client to send all other non-transaction-related Web3 requests.
- `address_index`: `number`, optional. If specified, will tell the provider to manage the address at the index specified. Defaults to the first address (index `0`).
- `password`: `string`, optional. If specified, will derive seed with addition of said bip39 passphrase.
## Truffle Usage

You can easily use this within a Truffle configuration. For instance:

truffle.js
```javascript
var HDWalletProvider = require("truffle-safe-hdwallet-provider");

var mnemonic = "opinion destroy betray ...";

module.exports = {
  networks: {
    development: {
      host: "localhost",
      port: 8545,
      network_id: "*" // Match any network id
    },
    ropsten: {
      provider: new HDWalletProvider(mnemonic, "https://ropsten.infura.io/"),
      network_id: 3
    }
  }
};
```
