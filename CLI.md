# Metaplex Command line interface 
## Description
Installing this tools will allow you to use Metaplex functionnality, without the store to spin up a store, very useful.
At the end of this tutorial you will be able to mint 
## Prerequisite

To be able to start creating your own NFT massively, you need to install these packages 

- yarn
- [Solana CLI](https://docs.solana.com/cli/install-solana-cli-tools)


Once these packages installed, you must be able to use the solana CLI using
```solana -h```

## Installation

- Clone this repo
- Navigate into it by using ```cd metaplex-goodpick/js/packages/cli```
- Run ```yarn install```
- Then ```yarn build```
- Then ```yarn run package:macos``` or  ```yarn run package:linux``` depending on your system OS (not tested on windows yet)

Some people have trouble with yarn run package:macos
If it’s not working for you, the common workaround has been
npx pkg . -d --targets node14-macos-x64 --output bin/macos/metaplex

Then you'll be able to use the metaplex command line interface 
You can try using it by typing
```metaplex -h```

