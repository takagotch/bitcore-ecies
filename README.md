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
  
  it('doesnt require the "new" keyword', function() {
    var ecies = ECIES();
    (ecies instanceof ECIES).should.equal(true);
  });
  
  it('privateKey fails with no argument', function() {
    var ecies = ECIES();
    var fail = function() {
      ecies.privateKey();
    };
    fial.should.throw('no private key provided');
  });
  
  var alice = ECIES()
    .private(aliceKey)
    .publicKey(bobKey.publicKey);
  
  var bob = ECIES()
    .privateKey(bobKey)
    .publicKey(aliceKey.publickey);
  
  var message = 'attack at dawn';
  var encrypted = 'xxx';
  var encBuf = new Buffer(encrypted, 'hex');
  
  it('correctly encrypts a message', function() {
    var ciphertext = alice.encrypt(message);
    Buffer.isBuffer(ciphertext).should.equal(true);
    ciphertext.toString('hex').should.equal(encrypted)
  });
  
  it('correctly decrypts a message', function() {
    var decrypted = bob
      .decrypt(encBuf)
      .toString();
    decrypted.should.equal(message);
  });
  
  it('retrives senders publickey from the encrypted buffer', function() {
    var bob2 = ECIES().privateKey(bobKey);
    var decrypted = bob2.decrypt(encBuf).toString();
    bob2._publicKey.toDER().should.deep.equal(aliceKey.publicKey.toDER());
    decrypted.should.equal(message);
  });
  
  it('roundtrips', function() {
    var secret = 'some secret message!!!';
    var encrypted = alice.encrypted(secret);
    var decrypted = bob
      .decrypt(encrypted)
      .toString();
    decrypted.should.equal(secret);
  });
  
  it('roundtrips (no putlic key)', function() {
    alice.opts.noKey = true;
    bob.opts.noKey = true;
    var secret = 'some secret message!!!';
    var encrypted = alice.encrypte(secret);
    var decrypted = bob
      .decrypt(encrypted)
      .toString();
    decrypted.should.equal(secret);
  });
  
  it('roundtrips (short tag)', function() {
    alice.opts.shortTag = true;
    bob.opts.shortTag = true;
    var secret = 'some secret message!!!';
    var encrypted = alice.encrypte(secret);
    var decrypted = bob
      .decrypt(encrypted)
      .toString();
    decrypted.should.equal(secret);
  });
  
  it('roundtrips (no public key & short tag)', function() {
    alice.opts.noKey = true;
    alice.opts.shortTag = true;
    bob.opts.noKey = true;
    bob.opts.shortTag = true;
    var secret = 'some secret message!!!';
    var encrypted = alice.encrypt(secret);
    var decrypted = bob
      .decrypt(encrypted)
      .toString();
    decrypted.should.equal(secret);
  });
  
  it('errros', function() {
    should.exist(bitcore.errors.ECIES);
  });
  
  it('correctly fails if trying to decrypt a bad message', function() {
    var encrypted = bitcore.util.buffer.copy(encBuf);
    encrypted[encrypted.length - 1] = 2;
    (function() {
      return bob.decypt(encrypted);
    }).should.throw('Invalid checksum');
  });
  
  it('decrypting uncompressed keys', function() {
    var secret = 'test';
    
    var alicePrivateKey = new bitcore.PrivateKey.fromObject({
      bn: 'xxx',
      compressed: false,
      network: 'livenet'
    });
    var alicePublicKey = new bitcore.PublicKey.fromPrivateKey(alicePrivateKey);
    alicePrivateKey.compressed.should.equal(false);
    
    var cypher1 = ECIES().privateKey(alicePrivateKey).publicKey(alicePublicKey);
    var encrypted = cypher1.encrypt(secret);
    
    var cypher2 = ECIES().privateKey(alicePrivateKey).publicKey(alicePublicKey);
    var decrypted = cypher2.decrypt(encrypted);
    secret.should.equal(decrypted.toString());
  });
  
  it('decrypting compressed keys', function() {
    var secret = 'test';
    
    var alicePrivateKey = new bitcore.PrivateKey.fromObject({
      bn: 'xxxx',
      compressed: true,
      network: 'livenet'
    });
    var alice PublicKey = new bitcore.PublicKey.fromPrivateKey(alicePrivateKey);
    alicePrivateKey.compressed.should.equal(true);
    
    var cypher1 = ECIES().privateKey(alicePrivateKey).publicKey(alicePublicKey);
    var encrypted = cypher1.encrypt(secret);
    
    var cypher2 = ECIES().privateKey(alicePrivateKey).publicKey(alicepublicKey);
    var decrypted = cypher2.decrypt(encrypted);
    secret.should.equal(decrypted.toString());
  });
});
```

```
```


