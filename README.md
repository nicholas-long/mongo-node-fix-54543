# mongo-node-fix-54543

fix data issues in mongo caused by node.js - extract broken objects from mongo BSON and output as JSON.

- node issue: https://github.com/nodejs/node/issues/54543
  - affects node version 22.7.0 - related to optimization code paths for utf8 encoding, causing it to fail after encoding a few thousand utf8 strings.
- created CLI tool `identify-utf8-errors.js` to find and remove the broken documents by ID. return JSON as backup.
- fix for issue: update node.js version from `22.7.0` for all clients writing to mongo.
  - any documents accidentally written before this upgrade can be fixed using this script.

# requirements

- `mongodb` NPM package

# Usage

```bash
npm install mongodb

node identify-utf8-errors.js (mongo URL) (db name) (collectionname)
```

- all broken documents are always written as JSON into file `recovered.json`

## arguments

```js
const url = process.argv[2]
const database = process.argv[3]
const collectionname = process.argv[4]
```

## option flags

- `--delete` - remove all broken documents
- `--backup` - create backup BSON file (JSON data file is always created for backups)
- `--quiet` - suppress printing messages with offest counts of broken documents
