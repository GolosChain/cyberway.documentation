# How To Create Key Pair

### Goal
Create a public and private key pair for signing transactions.

### Before you begin
  * Install the currently supported version of `cleos`.
  * Understand the following:
    * What is a [public](https://docs.cyberway.io/users/glossary#public-key) and [private](https://docs.cyberway.io/users/glossary#private-key) key pair.

### Steps
To output the key pair to the console
```sh
$ cleos create key --to-console
```

To save the key pair to file
```sh
$ cleos create key --file FILE_TO_SAVEKEY
```