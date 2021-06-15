anacl-js
========

[![Build Status](https://travis-ci.org/codesnug/anacl-js.svg?branch=anacl-1.0.3)](https://travis-ci.org/codesnug/anacl-js)

A [TweetNaCl.js](https://github.com/dchest/tweetnacl-js) fork for asynchronous PRNGs.

The following methods which rely on the asynchronous PRNG are changed to return `Promise`:

* `nacl.randomBytes`
* `nacl.box.keyPair`
* `nacl.sign.keyPair`

The followings are the default PRNGs used, depending on the platform anacl runs on:

* `window.crypto.getRandomValues` (WebCrypto standard)
* `window.msCrypto.getRandomValues` (Internet Explorer 11)
* `crypto.randomBytes` (Node.js)
* `wx.getRandomValues` (WeChat)

If the above are not available on the platform you are targeting, and you have a cryptographically-strong source of
entropy, you can plug it in like this:

```javascript
nacl.setPRNG(function(x, n) {
  // ... copy n random bytes into x, synchronously or asynchronously (return a promise) ...
});
```

Other than the above, check [TweetNaCl.js](https://github.com/dchest/tweetnacl-js) for usage in general.
