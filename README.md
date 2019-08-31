### bitcore-ecies
---
https://github.com/bitpay/bitcore-ecies

```js
var alice = ECIES()
  .privateKey(aliceKey)
  .publicKey(bobKey.publicKey);
  
var message = 'some secret message';
var encrypted = alice.encrypt(message);

var bob = ECIES()
  .privateKey(bobKey)
  .publicKey(aliceKey.publicKey);
var decrypted = bob
  .decrypt(encrypted)
  .toString();
```

```js
// test/ecies.js

describe('ECIES', function() {
  
  it('ECIES', function() {
    (typeof ECIES).should.equal('function');
  });
  
  it('constructs an instance', function() {
    (typeof ECIES).should.equal('function');
  });
  
  it('constructs an instance', function() {
    var ecies = new ECIES();
    (ecies instanceof ECIES).should.equal(true);
  });
  
  
  
  
  
});
```

```
```


