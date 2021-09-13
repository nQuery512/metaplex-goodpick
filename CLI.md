# Metaplex Command line interface 
## Description
Installing this tools will allow you to use Metaplex functionnality, without the store to spin up a store, very useful.
At the end of this tutorial you will be able to prepare everything to be able to build a fair launch using the Metaplex Candy Machine.
## Prerequisite

To be able to start creating your own NFT massively, you need to install these packages 

- [node/NPM]()
- [yarn](https://classic.yarnpkg.com/en/docs/install/#windows-stable)
- [Solana CLI](https://docs.solana.com/cli/install-solana-cli-tools)

You should also own some $SOL in order to go through this tutorial, we are gonna do the walktrough using the devnet, but the same process apply for every network
To get $SOL on devnet/testnet it's [HERE](https://solfaucet.com/) 

Once these packages installed, you must be able to use the solana CLI using
```solana -h```


Since the upload coast is based on the size of your files, you should optimize the size of your files! 

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

In the following tutorial, if a Metaplex command is not clear, you can just do ``` metaplex help [COMMAND]```, for exemple: ```metaplex help upload```.

It'll show you a description of the function and the available parameters

## Wallet configuration (optional)
You should have configured the same wallet on phantom and the solana cli in order to simplify this process,

This is required if you want to give you some NFTs using the mint_one_command() Metaplex CLI function, but you can do it also from the frontend without the need to do this section 

COMING SOON


## File and Metadata
### Description

In this part I will explain about how files and metadata should be done! 

Arweave is the file hosting blockchain that most project use on Solana, it's similar to IPFS and allow files to be store in a decentralized way.
We will be using Metaplex CLI to upload our file on Arweave

Metadata defines your file and should be correctly setup, in most case, their is no way for you to modify them after upload, you'll have to upload them again

You'll be able to find an Arweave fee calculator based on the size of the files you want to upload, see [HERE](https://55mcex7dtd5xf4c627v6hadwoq6lgw6jr4oeacqd5k2mazhunejq.arweave.net/71giX-OY-3LwXtfr44B2dDyzW8mPHEAKA-q0wGT0aRM)

### Metadata template

Metaplex Metadata full documentation can be found [here](https://docs.metaplex.com/nft-standard), I HIGHLY recommand that you read it and keep it while building your metadata,

For each distinct NFT you plan to create, you need to create a .json file similar to this one

```
{
  "name": "Test NFT #1",
  "symbol": "TOTO",
  "description": "Run test",
  "seller_fee_basis_points": 0,
  "image": "0.png",
  "edition": "2021 limited edition",
  "attributes": [
    {
      "trait_type": "rarity",
      "value": "epicc"
    },
    {
      "trait_type": "color",
      "value": "diamond"
    }
  ],
  "properties": {
    "category": "image",
    "creators": [
      {
        "address": "H3j6mUMJa64kuDSqi5rmLxYqrDmU4nVd4jiTkezy7zEM",
        "share": 100
      }
    ],
    "files": [
      {
        "uri": "https://www.arweave.net/FvJ0iDYtwE-VoeiGJ4SsJI-0W_9lSL6ZtZDMU57X7m4?ext=png",
        {"uri":"0.png", "type":"image/png"}
      }
    ]
  }
}
```


You should go into your metaplex directory (where you cloned this repository),
Personally, I created a directory in the metaplex folder named 'assets' and I've put all my file and metadata in there, so if you didn't
you'll need to change the following commands.

### File Preparation
/!\ **Warning**: At the moment (13/09/21), there is no way to upload other files than .png and .json for source files, if this isnt correctly patched soon,
we will deploy our own patch.


In this assets directory, you should put all the files (JSON and IMG)
### Start upload
First, let's upload our files, be carefull, this is the part that cost you money,
The program do a SOL swap to AR which is the currency of the Arweave blockchain to be able to upload your files to the Arweave FS
Then it sends your file.

Let's run the following command:

```
metaplex upload ~/metaplex_good/assets --keypair ~/.config/solana/devnet.json --env devnet
```

The first argument is your asset path, 

Then --keypair is the path of your keypair usually located in ~/.config/solana/ where ~ is your home directory (/home/dev/ for exemple)

The third argument is the network you want to use, here we are using devnet

When the command succeed, you should see something like this :

```
// Here I have uploaded 4 images, named from 0.png to 3.png, same for metadata 0.json, 1.json... so I had 8 files in the assets folder ! 
setting cache for 3
Writing indices 0-3
Done. Successful = true. If 'false' - rerun
```

You should look into the full logs printed to your console, to see if anything went wrong,
Also, you are able to read the cache to find every informations needed, it's print a synthetized json with info on each sets and it also show upload link of each images
(We plan to releasing a script to help you getting all the upload link)

Note: If some uploads doesn't succeed that's not uncommon, in fact, when you upload massively, it'll happen, but we got you covered.

What you need to do is to relaunch the same command.

Since Metaplex is using a cache in ~/metaplex_goodpick/.cache, it keep tracks of which files succeed to be uploaded and the one who fails
That means that once a file is correctly uploaded, you can restart the command to upload the files who failed and the good one will be skipped, you will not have to pay for them again and they won't be uploaded, 

After uploaded correctly, your upload should look like this on [arweave](https://jw4aqnpgl6gt3ma7dnfmhrbz62knne7uoly3ypxwkfejnlkf27ia.arweave.net/TbgINeZfjT2wHxtKw8Q59pTWk_Ry8bw-9lFIlq1F19A/)


### Candy machine preparation
Now that out file have been correctly uploaded, we are able to setup the candy machine, it's the program that will allow your website to enable the "mint by user" functionnality.

In this section we will use 2 command of the metaplex CLI to, first, enable your candy-machine with a mint price (what will the user will pay to mint on your website), then to set a start data to your mint.

#### Enable the candy machine
In the metaplex directory, run the following command:
```metaplex create_candy_machine --price 0 --keypair ~/.config/solana/devnet.json```
You can specify the price user pays in $SOL with the --price argument 

Run the command, you should see an output in your terminal similar to this one:

```
create_candy_machine Done: **AE1zUCxpmPDeL3nKY95sSSETwkSYo93Ps14NiCRJ9YeA**
```

**KEEP THIS ID**, it'll be required further in this guide in order to connect your frontend to the candy-machine you just created ! 

You can use the command ```metaplex verify --keypair ~/.config/solana/devnet.json ``` to check if the mint 
It'll print the state of each upload with the state of the candy-machine !

