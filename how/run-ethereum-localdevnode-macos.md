# How to set up local Ethereum node on macOS

```
TODO:
. make guide OS agnostic
  . extend for linux
  . extend for Windows
  . extend for Nix?
```

# overview

The purpose of this guide is to install a bare-bones local Ethereum development node with macOS. Barebones means that we will not be using a framework like Hardhat or Truffle.

We will install geth (geth for 'Go Ethereum') which is the official Ethereum client CLI suite. Geth is cool because it comes with a javascript console for interacting with the chain via the web3.js API.

Running a full node on mainnet is expensive (need ~500GB free space), and we have to use real eth, so we will focus on a local development node.

To be clear, to 'install a local node', is to create a brand new Ethereum blockchain on your computer.

The order of operations will go like this:

1. get geth

2. setup new blockchain

3. run new blockchain with local devnode

4. connect to node with client and do some stuff

5. outro


# 1. get geth

First we need geth. 

[If you don't have homebrew, you first need to install it by following the guide at this link.](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-homebrew-on-macos)

Use homebrew to install geth:
```
brew tap ethereum/ethereum
brew install ethereum
```

Verify the install by running ```geth version```, which should return something like this:
```
blairmunroakusa$ geth version
 Geth
 Version: 1.10.16-stable
 Architecture: amd64
 Go Version: go1.17.6
 Operating System: darwin
 GOPATH=
 GOROOT=go
```

And this is geth. With this tool installed, we can not only manipulate a local dev node, but we can also connect and interact with the Ethereum mainnet, accounts, smartcontracts, etc.


# 2. setup new blockchain

The first thing we need to do is set up the genesis block, which in general is the first block on any blockchain.

We will be using a tool called puppeth, which is bundled into geth.

Navigate to a new private space on your local machine, then run ```puppeth```:
```
mkdir interlockdev-ethereum
cd interlockdev-ethereum
mkdir devnode1
mkdir devnode2
puppeth
```

This will take us through the following setup prompt menu to configure a new genesis block.

Choose a network name:
```
blairmunroakusa$ puppeth
.
. <intro placcard here>
.

Please specify a network name to administer (no spaces, hyphens or capital letters please)
> interlockdev
```

Configure new genesis:
```
What would you like to do? (default = stats)
 1. Show network stats
 2. Configure new genesis
 3. Track new remote server
 4. Deploy network components
> 2
```

Create ours from scratch:
```
What would you like to do? (default = create)
 1. Create new genesis from scratch
 2. Import already existing genesis
> 1
```

>_As of writing, 17Mar22, Ethereum mainnet is running a proof-of-work consensus algorithm, with a transition to proof-of-stake consensus sometime Q1-Q2, 2022._

We will create a proof-of-work chain.

Choose proof-of-work:
```
Which consensus engine to use? (default = clique)
 1. Ethash - proof-of-work
 2. Clique - proof-of-authority
> 1
```

Disregard prefunding account:
```
Which accounts should be pre-funded? (advisable at least one)
> 0x
(not pre-funding any)
```

>_Note, accounts in ethereum are 40 digit hexadecimal numbers._

Do what is advisable:
```
Should the precompile-addresses (0x1 .. 0xff) be pre-funded with 1 wei? (advisable yes)
> yes
```

Specify default network ID:
```
Specify your chain/network ID if you want an explicit one (default = random)
> 1234
```

Choose manage genesis we just created above:
```
What would you like to do? (default = stats)
 1. Show network stats
 2. Manage existing genesis
 3. Track new remote server
 4. Deploy network components
> 2
```

Export config for new genesis block:
```
 1. Modify existing configurations
 2. Export genesis configurations
 3. Remove genesis configuration
> 2
```

And finally, save to ```interlockdev-ethereum``` directory:
```
Which folder to save the genesis specs into? (default = current)
>
(no selection is default)
```

Okay cool. Our blockchain genesis block is setup. Exit out of ```puppeth```. Your ```interlockdev-ethereum``` directory should have the following json files:
```
blairmunroakusa$ ls
 devnode1
 devnode2
 interlockdev-aleth.json
 interlockdev-harmony.json
 interlockdev-parity.json
 interlockdev.json
 ```


# 3. run new blockchain with local devnode

We start by initializing a single node. This ```init``` command will create a ```keystore``` directory for private keys, and a ```geth``` (containing ```chaindata```) directory for general blockchain and node data. We will be setting up ```devnode1``` as the primary node that runs the blockchain.

From ```interlockdev-ethereum``` run:
```
geth --datadir devnode1 init interlockdev.json
```

Now we need to create an account that represents this node. This is the default etherbase.

>_The etherbase or coinbase is the account that mining proceeds are deposited in._

From ```interlockdev-ethereum``` run:
```
geth --datadir devnode1 account new
```

Create a password as prompted (remember it), and copy the account address for future reference. Mine is ```0x2402c3fe2f60e3cdc951c61450dd0c80aa0baeb5```. Save the password in a file within ```devnode1``` directory:
```
echo <mypastedpassword> > devnode1/password.sec
```

Your ```devnode1``` directory should now look like this:
```
blairmunroakusa$ ls
 geth
 keystore
 password.sec
 ```

OK

It's time to fire up the blockchain, originating at ```devnode1```:
```
geth --networkid 1234 --mine --miner.threads 1 --http.api web3,eth,personal,net --unlock 0 --nodiscover --datadir devnode1 --password devnode1/password.sec --ipcpath ~/Library/Ethereum/geth.ipc
```

> _Default RPC port is 8545. Default listening port is 30303._

At this point you may see a streaming list of
```
INFO [date] Generating DAG in progress
```

which will eventually transition to
```
INFO [date] 🔨 mined potential block
INFO [date] Commit new sealing work 
```

This means your machine is maintaining an Ethereum blockchain and the node is mining to verify any transactions which might occur (none so far). The account we made earlier is our primary account, or our _etherbase_ or _coinbase_ which is where this blockchain will deposit ether earned by mining a block. We can specify a different etherbase at any time.

If you need to stop the blockchain process, you can always restart it later and the process will resume at it's final state.

Now it's time to...


# 4. connect to node with client and do some stuff

Open a new terminal session, leaving the blockchain process running (that or just run the process in the background instead). Now we want to connect to the node by firing up a javascript console. This is easy. Run:
```
geth attach
```

Now we can fire off web3, eth, and personal commands to interact with the blockchain.

First, check to see which accounts are active. It should only be the etherbase:
```
> eth.accounts
["0x2402c3fe2f60e3cdc951c61450dd0c80aa0baeb5"]
```

Yup, that was my etherbase account.

Now let's get the etherbase balance:
```
> web3.fromWei(eth.getBalance(eth.accounts[0]), "ether")
126
```

This command gets the balance of account 0 in wei, and converts it into ether. There are 1,000,000,000,000,000,000 (10^18) wei in one ether, so it is nice to convert things to ether first.

Really quick, let's create an account now and transfer some ether to it.
```
> personal.newAccount()
```

Choose a password, now we have
```
> eth.accounts
["0x2402c3fe2f60e3cdc951c61450dd0c80aa0baeb5", "0x83c257547034b056b23b0807f967045d2b59af4b"]
```

but unfortunately something sad:
```
> web3.fromWei(eth.getBalance(eth.accounts[1]), "ether")
0
```

So let's finish up the hands-on by creating a transfer transaction:
```
> eth.sendTransaction({from: eth.accounts[0], to: eth.accounts[1], value: 200000000000000})
"0x53c3acf3333cd4a35d3b7752746c449974bc96b84729dca751b4a2304f8c4b88"
> web3.fromWei(eth.getBalance(eth.accounts[1]), "ether")
0.0002
```

It's not much, but sometimes 0.0002 eth between friends really is better than nothing.

The long hex number is the transaction hash.


# 5. outro

And that's that. If you've been following along, you just configured a private Ethereum blockchain and got it running with a single local node on your machine.

Next time, we will review how to set up additional nodes on a private Ethereum dev blockchain.
