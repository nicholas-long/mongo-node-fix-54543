# mongo-node-fix-54543
fix data issues in mongo caused by node.js - extract broken objects from BSON and output as JSON

- node issue: https://github.com/nodejs/node/issues/54543
  - affects node version 22.7.0 - related to optimization code paths for utf8 encoding, causing it to fail after encoding a few thousand utf8 strings.
