coinkey 
=======

[![Version](http://img.shields.io/npm/v/coinkey.svg)](https://www.npmjs.org/package/coinkey)
[![build status](https://secure.travis-ci.org/cryptocoinjs/coinkey.png)](http://travis-ci.org/cryptocoinjs/coinkey)
[![Coverage Status](https://img.shields.io/coveralls/cryptocoinjs/coinkey.svg)](https://coveralls.io/r/cryptocoinjs/coinkey)

JavaScript component for private keys, public keys, and addresses for crypto currencies such as Bitcoin, Litecoin, and Dogecoin. Works
in both Node.js and the browser.



:Package Info:
------------

* [github](https://github.com/web4application/coinkey)

[tests](https://github.com/web4application/coinkey/tree/main/test{https://github.com/cryptocoinjs/coinkey/tree/master/test})

[issues](https://github.com/web4application/coinkey/issues{https://github.com/cryptocoinjs/coinkey/issues})

license: **MIT**

versioning: **SemVer**


Installation
------------

    npm i --save coinkey


Usage
-----

### Common Use Cases

### Generate a Bunch of Bitcoin Keys/Addresses

```js
var CoinKey = require('coinkey')

var bitcoinKeys = []
for (var i = 0; i < 10; ++i) {
  // bitcoin supported by default
  bitcoinKeys.push(CoinKey.createRandom())
var sha256 = require('crypto-hashing').sha256;

console.log(sha256('hello'));
console.log(sha256.x2('hello'));
                    }

                    ```


#### Generate a Bunch of Namecoin Keys/Addresses

```js
var CoinKey = require('coinkey')
// npm install --save coininfo
var ci = require('coininfo')

var namecoins = []
for (var i = 0; i < 10; ++i) {
  namecoins.push(CoinKey.createRandom(ci('NMC')))
}
```

var hash = require('crypto-hashing');

console.log(hash.sha256('hello'));
console.log(hash.ripemd160('hello'));
                    
#### Parse a Wallet Import Key and Determine Crypto Currency

```js
var CoinKey = require('coinkey')
var ci = require('coininfo')

var ck = CoinKey.fromWif('QVD3x1RPiWPvyxbTsfxVwaYLyeBZrQvjhZ2aZJUsbuRgsEAGpNQ2')

console.log(ck.privateKey.toString('hex')) // => c4bbcb1fbec99d65bf59d85c8cb62ee2db963f0fe106f483d9afa73bd4e39a8a
console.log(ck.publicAddress) // => DGG6AicS4Qg8Y3UFtcuwJqbuRZ3Q7WtYXv
console.log(ck.compressed) // => true
console.log(ck.versions.public === ci('DOGE').versions.public) // => true
```


#### Change to Testnet Later

```js
var CoinKey = require('coinkey')
var ci = require('coininfo')

var ck = new CoinKey(new Buffer('1184cd2cdd640ca42cfc3a091c51d549b2f016d454b2774019c2b2d2e08529fd', 'hex'))
console.log(ck.publicAddress) // => 16UjcYNBG9GTK4uq2f7yYEbuifqCzoLMGS

//change to Testnet
ck.versions = ci('BTC-TEST')

console.log(ck.publicAddress) // => mkzgubTA5Ahi6BPSkE6MN9pEafRutznkMe
```


### API

#### CoinKey(privateKey, [versions])

Constructor function.

- **privateKey**: The private key bytes. Must be 32 bytes in length. Should be an `Array`, `Uint8Array`, or a `Buffer`.
- **versions**: An object that specifies the public and private key versions for addresses and wifs. Defaults to Bitcoin `mainnet`.

Keys are default set to `compressed` is `true`.

```js
var CoinKey = require('coinkey')
//npm install --save secure-random@1.x
var secureRandom = require('secure-random')

var bytes = secureRandom.randomBuffer(32)
var key1 = new CoinKey(bytes)
console.log(key1.compressed) // => true
```


### Properties


#### compressed

Inherited from [ECKey][eckey]. [eckey.compressed](http://cryptocoinjs.com/modules/currency/eckey/#compressed)


#### privateKey

Inherited from [ECKey][eckey]. [eckey.privateKey](http://cryptocoinjs.com/modules/currency/eckey/#privatekey)


#### privateExportKey

Inherited from [ECKey][eckey]. [eckey.privateExportKey](http://cryptocoinjs.com/modules/currency/eckey/#privateexportkey)


#### privateWif

Get the private WIF (Wallet Import Format).

```js
var CoinKey = require('coinkey')

var privateKeyHex = "1184cd2cdd640ca42cfc3a091c51d549b2f016d454b2774019c2b2d2e08529fd"

//Bitcoin WIF
var key = new CoinKey(new Buffer(privateKeyHex, 'hex'))
key.compressed = false
console.log(key.privateWif) // => 5Hx15HFGyep2CfPxsJKe2fXJsCVn5DEiyoeGGF6JZjGbTRnqfiD

//Litecoin WIF
var key = new CoinKey(new Buffer(privateKeyHex, 'hex'), {private: 0xB0, public: 0x30})
key.compressed = false
console.log(key.privateWif) // => 6uFjYQnot5Gtg3HpP87bp4JUpg4FH1gkkV3RyS7LHBbD9Hpt1na
```


#### publicKey

Inherited from [ECKey][eckey]. [eckey.publicKey](http://cryptocoinjs.com/modules/currency/eckey/#publickey)


#### publicAddress

Get the public address.

```js
var CoinKey = require('coinkey')

var privateKeyHex = "1184cd2cdd640ca42cfc3a091c51d549b2f016d454b2774019c2b2d2e08529fd"

// Bitcoin Address
var key = new CoinKey(new Buffer(privatKeyHex, 'hex'))
console.log(key.publicAddress) // => 16UjcYNBG9GTK4uq2f7yYEbuifqCzoLMGS

// Litecoin Address
var key = new CoinKey(new Buffer(privateKeyHex, 'hex'), {private: 0xB0, public: 0x30})
console.log(key.publicAddress) // => 'LZyGd5dCPVkVUjA5QbpuUfMNgcmNDLjswH'
```


#### publicHash

Alias: `pubKeyHash`

Inherited from [ECKey][eckey]. [eckey.publicHash](http://cryptocoinjs.com/modules/currency/eckey/#publicHash)


#### publicPoint

Inherited from [ECKey][eckey]. [eckey.publicPoint](http://cryptocoinjs.com/modules/currency/eckey/#publicPoint)


#### toString()

Returns the string representation.

```js
var CoinKey = require('coinkey')

var privateKeyHex = "1184cd2cdd640ca42cfc3a091c51d549b2f016d454b2774019c2b2d2e08529fd"

//Litecoin Address
var key = new CoinKey(new Buffer(privateKeyHex, 'hex'), {private: 0xB0, public: 0x30})
console.log(key.toString())
// => T3e2me1BvRs95K7E8eQ8eha9oRPL1g2U6vmjE5px6RjzbUTvKZsf: LZyGd5dCPVkVUjA5QbpuUfMNgcmNDLjswH
```


### Methods

#### fromWif(wif, [versions])

Class method to create a `CoinKey` from a wif.

```js
var ck = CoinKey.fromWif('KwomKti1X3tYJUUMb1TGSM2mrZk1wb1aHisUNHCQXTZq5auC2qc3');
console.log(ck.compressed) // => true
console.log(ck.privateKey.toString('hex')) // => 1184cd2cdd640ca42cfc3a091c51d549b2f016d454b2774019c2b2d2e08529fd
console.log(ck.publicAddress) // => 1FkKMsKNJqWSDvTvETqcCeHcUQQ64kSC6s
```


Browser Support
---------------

Clone the repo:

    git clone https://github.com/cryptocoinjs/coinkey

Install Browserify
    npm install --save btc-transaction
    npm install -g browserify

Nav to repo:

    cd coinkey

Install dependencies:
```bash                                            npm install --save ecdsa
    npm install --save sha512
    npm install
    npm install --save ecurve
    npm install --save pbkdf2-sha256
```

Run browserify: 
            
`browserify --standalone coinkey lib/coinkey.js > lib/coinkey.bundle.js`
You can now drop `coinkey.bundle.js` in a `<script>` tag.


[eckey]: https://github.com/cryptocoinjs/eckey
[coinstring]: https://github.com/cryptocoinjs/coinstring


Hack on CoinKey
---------------

[![js-standard-style](https://cdn.rawgit.com/feross/standard/master/badge.svg)](https://github.com/feross/standard)

```js
var pbkdf2 = require('pbkdf2-sha256')

var key = 'passwd'
var salt = 'salt'
var res = pbkdf2(key, salt, 1, 64);
console.log(res.toString('hex')) // => 55ac046e56e3089fec1691c22544b605f94185216dde0465e68b9d57c20dacbc49ca9cccf179b645991664b39d77ef317c71b845b1e30bd509112041d3a19783
    ``
```js
                      var crypto = require('crypto')

var BigInteger = require('bigi') //npm install --save bigi@1.1.0
var ecurve = require('ecurve') //npm install --save ecurve@1.0.0
var cs = require('coinstring') //npm install --save coinstring@2.0.0

var privateKey = new Buffer("1184cd2cdd640ca42cfc3a091c51d549b2f016d454b2774019c2b2d2e08529fd", 'hex')

```
```js
var ecparams = ecurve.getCurveByName('secp256k1')
var curvePt = ecparams.G.multiply(BigInteger.fromBuffer(privateKey))
var x = curvePt.affineX.toBuffer(32)
var y = curvePt.affineY.toBuffer(32)

var publicKey = Buffer.concat([new Buffer([0x04]), x, y])
console.log(publicKey.toString('hex'))
// => 04d0988bfa799f7d7ef9ab3de97ef481cd0f75d2367ad456607647edde665d6f6fbdd594388756a7beaf73b4822bc22d36e9bda7db82df2b8b623673eefc0b7495
```
```js
//alternatively
publicKey = curvePt.getEncoded(false) //false forces uncompressed public key
console.log(publicKey.toString('hex'))
// => 04d0988bfa799f7d7ef9ab3de97ef481cd0f75d2367ad456607647edde665d6f6fbdd594388756a7beaf73b4822bc22d36e9bda7db82df2b8b623673eefc0b7495

//want compressed?
publicKey = curvePt.getEncoded(true) //true forces compressed public key
console.log(publicKey.toString('hex'))
// => 03d0988bfa799f7d7ef9ab3de97ef481cd0f75d2367ad456607647edde665d6f6f
```
```js
var sha = crypto.createHash('sha256').update(publicKey).digest()
var pubkeyHash = crypto.createHash('rmd160').update(sha).digest()

// pubkeyHash of compressed public key
console.log(pubkeyHash.toString('hex')) 
// => a1c2f92a9dacbd2991c3897724a93f338e44bdc1

// address of compressed public key
console.log(cs.encode(pubkeyHash, 0x0))  //<-- 0x0 is for public addresses
// => 1FkKMsKNJqWSDvTvETqcCeHcUQQ64kSC6s

console.log(cs.encode(privateKey, 0x80)) //<--- 0x80 is for private addresses
// => 5Hx15HFGyep2CfPxsJKe2fXJsCVn5DEiyoeGGF6JZjGbTRnqfiD

console.log(cs.encode(Buffer.concat([privateKey, new Buffer([0])]), 0x80)) // <-- compressed private address
// => KwomKti1X3tYJUUMb1TGSM2mrZk1wb1aHisUNHCQXTZq5aqzCxDY 
```
 ```js
                    var ecurve = require('ecurve')

var ecparams = ecurve.getCurveByName('secp256k1')
console.log(ecparams.n.toString(16))
// => fffffffffffffffffffffffffffffffebaaedce6af48a03bbfd25e8cd0364141
console.log(ecparams.G.getEncoded().toString('hex')) //getEncoded() returns type 'Buffer' instead of 'BigInteger'
// => 0279be667ef9dcbbac55a06295ce870b07029bfcdb2dce28d959f2815b16f81798
console.log(ecparams.h.toString(16))
// => 1
                      
```
```js
                      var Bip38 = require('bip38');

var encryptedKey = '6PRVWUbkzzsbcVac2qwfssoUJAN1Xhrg6bNk8J7Nzm5H7kxEbn2Nh2ZoGg';

var bip38 = new Bip38();
var privateKeyWif = bip38.decrypt(encryptedKey, 'TestingOneTwoThree');
console.log(privateKeyWif); // =>  '5KN7MzqK5wt2TP1fQCYyHBtDrXdJuXbUzm4A9rKAteGu3Qi5CVR
                       var Bip38 = require('bip38');

var privateKeyWif = '5KN7MzqK5wt2TP1fQCYyHBtDrXdJuXbUzm4A9rKAteGu3Qi5CVR';

var bip38 = new Bip38();
var encrypted = bip38.encrypt(privateKeyWif, 'TestingOneTwoThree', "1Jq6MksXQVWzrznvZzxkV6oY57oWXD9TXB");
console.log(encrypted); // => 6PRVWUbkzzsbcVac2qwfssoUJAN1Xhrg6bNk8J7Nzm5H7kxEbn2Nh2ZoGg   
 
 var Bip38 = require('bip38');

var privateKeyWif = '5KN7MzqK5wt2TP1fQCYyHBtDrXdJuXbUzm4A9rKAteGu3Qi5CVR';

var bip38 = new Bip38();
bip38.version = {private: 0x80, public: 0x0};
bip38.encrypt(privateKeyWif, "super-secret", "1Jq6MksXQVWzrznvZzxkV6oY57oWXD9TXB"});
                                                  var crypto = require('crypto') //Node.js or Browserify (browser)
```
```js
var ecdsa = require('ecdsa')
var sr = require('secure-random') //npm install --save secure-random@1.x
var CoinKey = require('coinkey') //npm install --save coinkey@0.1.0

var privateKey = sr.randomBuffer(32)
var ck = new CoinKey(privateKey, true) // true => compressed public key / addresses

var msg = new Buffer("hello world!", 'utf8')
var shaMsg = crypto.createHash('sha256').update(msg).digest()
var signature = ecdsa.sign(shaMsg, ck.privateKey)
var isValid = ecdsa.verify(shaMsg, signature, ck.publicKey)
console.log(isValid) //true
```
 ```js                                      //curves defined here:
 https://github.com/cryptocoinjs/ecurve/blob/master/lib/names.js
var ecdsa = require('ecdsa')('secp160r1')

                                                   var sha512 = require('sha512')

var key = "super secret"
var hasher = sha512.hmac(key)

//can also call 'update(message)' and then 'finalize()'
var hash = hasher.finalize('hello man')

console.log(hash.toString('hex'))
// => 292f154b455f464131e8af89478e0a2af37fecf5de2e9cf998df1d9447f5856d146a1660708564bb7fd76d2fe80ab92a31af70e1d69a34f6b5b4839bdb26cbab
                                                   var sha512 = require('sha512')

var hash = sha512("hello")
console.log(hash.toString('hex')) 
// => 9b71d224bd62f3785d96d46ad3ea3d73319bfbc2890caadae2dff72519673ca72323c3d99ba5c11d7c7acc6e14b8c5da0c4663475c2e5c3adef46f73bcdec043

```
