# Metaplex Command line interface 
## Description
Installing this tools will allow you to use Metaplex functionnality, without the store to spin up a store, very useful.
At the end of this tutorial you will be able to prepare everything to be able to build a fair launch using the Metaplex Candy Machine.
## Prerequisite

To be able to start creating your own NFT massively, you need to install these packages 

- [node/NPM]()
- [yarn](https://classic.yarnpkg.com/en/docs/install/#windows-stable)
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
```npx pkg . -d --targets node14-macos-x64 --output bin/macos/metaplex```

Then you'll be able to use the metaplex command line interface 
You can try using it by typing
```metaplex -h```

## Wallet configuration
You should have configured the same wallet on phantom and the solana cli in order to simplify this process
COMING SOON


## File and Metadata
### Description

In this part I will explain about how files and metadata should be done! 

Arweave is the file hosting blockchain that most project use on Solana, it's similar to IPFS and allow files to be store in a decentralized way.
We will be using Metaplex CLI to upload our file on Arweave

Metadata defines your file and should be correctly setup, in most case, their is no way for you to modify them after upload, you'll have to upload them again
This is the moment to talk about the upload cost

INSERT UPLOAD COST HERE

### Metadata template

Metaplex Metadata full documentation can be found [here](https://docs.metaplex.com/nft-standard), I HIGHLY recommand that you read it and keep it while building your metadata


For each distinct NFT you plan to create, you need to create a file similar to 



After uploaded correctly, your upload should look like this on [arweave](https://jw4aqnpgl6gt3ma7dnfmhrbz62knne7uoly3ypxwkfejnlkf27ia.arweave.net/TbgINeZfjT2wHxtKw8Q59pTWk_Ry8bw-9lFIlq1F19A/)
