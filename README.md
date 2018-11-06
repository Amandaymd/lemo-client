![Logo of the project](./logo.png)

# LemoChain JavaScript SDK
[![npm](https://img.shields.io/npm/v/lemo-client.svg?style=flat-square)](https://www.npmjs.com/package/lemo-client)
[![Build Status](https://img.shields.io/travis/lemo-client/lemo-client.svg?style=flat-square)](https://travis-ci.org/lemo-client/lemo-client)
[![code coverage](https://img.shields.io/coveralls/LemoFoundationLtd/lemo-client.svg?style=flat-square)](https://coveralls.io/r/LemoFoundationLtd/lemo-client)
[![install size](https://packagephobia.now.sh/badge?p=lemo-client)](https://packagephobia.now.sh/result?p=lemo-client)
[![gitter chat](https://img.shields.io/gitter/room/LemoFoundationLtd/lemo-client.svg?style=flat-square)](https://gitter.im/LemoFoundationLtd/lemo-client)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
[![GitHub license](https://img.shields.io/badge/license-LGPL3.0-blue.svg?style=flat-square)](https://github.com/LemoFoundationLtd/lemo-client/blob/master/LICENSE)

This is the LemoChain compatible JavaScript SDK which implements the Generic JSON RPC.


You need to run a local LemoChain node to use this library.

## Installing

### Using Yarn

```bash
yarn add lemo-client
```

### As Browser module

* Include `lemo-client.min.js` in your html file.
* Use the `LemoClient` object directly from global namespace:

## Example

```js
const LemoClient = require('lemo-client')
const lemo = new LemoClient({
    host: 'http://127.0.0.1:8001'
})

lemo.chain.getBlockByNumber(0)
    .then(function(block) {
        console.log(block)
    })
```

## LemoChain API
> NOTE: Every API returns a promise, except `watchXXX` which return `watchId` for stop watching

### chain
methods | description | available on http
---|---|---
lemo.getBlock(number, withTxList) | Get block by height (only stable block) | ✓
lemo.getBlock(hash, withTxList) | Get block by block hash | ✓
lemo.getCurrentBlock(false, withTxList) | Get the newest block | ✓
lemo.getCurrentBlock(true, withTxList) | Get the newest stable block | ✓
lemo.getCurrentHeight(false) | Get the newest block height | ✓
lemo.getCurrentHeight(true) | Get the newest stable block height | ✓
lemo.getGenesis() | Get the first block | ✓
lemo.getChainID() | Get the chain ID | ✓
lemo.getGasPriceAdvice() | Get transaction gas price advice | ✓
lemo.getNodeVersion() | Get the version of LemoChain node | ✓
lemo.getSdkVersion() | Get the version of lemo-client | ✓
lemo.watchBlock(withTxList, callback) | Listen for new block | ✓

### net
methods | description | available on http
---|---|---
lemo.net.addPeer(nodeAddr) | Connect to a peer | ✖
lemo.net.dropPeer(nodeAddr) | Disconnect to a peer | ✖
lemo.net.getPeers() | Get the connected peer list | ✖
lemo.net.getPeersCount() | Get the number of connected peers | ✓
lemo.net.getInfo() | Get the information of current LemoChain node | ✓

### mine
methods | description | available on http
---|---|---
lemo.mine.start() | Start mining | ✖
lemo.mine.stop() | Stop mining | ✖
lemo.mine.getMining() | True if current LemoChain node is mining | ✓
lemo.mine.getLemoBase() | Get the mining benefit account address of current LemoChain node | ✓

### account
methods | description | available on http
---|---|---
lemo.account.newKeyPair() | Create a private key and account address | ✖
lemo.account.getBalance(addr) | Get the balance of an account | ✓
lemo.account.getAccount(addr) | Get the information of an account | ✓

### tx
methods | description | available on http
---|---|---
lemo.tx.sendTx(privateKey, txInfo) | Sign and send transaction | ✓
lemo.tx.send(signedTxInfo) | Send a signed transaction | ✓
lemo.tx.sign(privateKey, txInfo) | Sign transaction | ✓
lemo.tx.watchPendingTx(callback) | Listen for the new Transaction | ✖


### other
methods | description | available on http
---|---|---
lemo.stopWatch(watchId) | Stop watching by watch ID | ✓
lemo.stopWatch() | Stop all watching | ✓
lemo.isWatching() | True if is watching some data | ✓


## Developing

### Requirements

* Node.js
* yarn

```bash
sudo apt-get update
sudo apt-get install nodejs
sudo apt-get install yarn
```

### Building

```bash
yarn build
```


### Configuration

There is some configuration in [lib/config.js](https://github.com/LemoFoundationLtd/lemo-client/blob/master/lib/config.js). It is useful for those who want build a private LemoChain

### Testing

```bash
yarn test
```

## Licensing

LGPL-3.0
