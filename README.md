# algorand-auction-cli

An interactive NodeJS CLI version of algorand auction-demo repo with Typescript. Also a byproduct of personal studying.
[algorand/auction-demo](https://github.com/algorand/auction-demo).

## Install

Do `yarn install` then `yarn build`.
This package will add two CLI commands: `algorand-auction-cli` and `algorand`
Starting with setting up an

### Trouble shooting

- [Permission denied for package after using yarn link](https://github.com/yarnpkg/yarn/issues/3587)

## CLI usage example

### Var

```shell
$AAC_USER            # username of current user
$AAC_ACCESSED_USERS  # list of users that have can be accessed
$AAC_AUCTION_ID      # auction id of current auction
$AAC_CLIENT_ID       # client id of current client
```

### Type and class

```shell
<str_num>      # parse 20k; 20m; 200_000; 2,000;
<auction_info> # auction info like start time and end time etc.
<client_id>    # client id, supposedly a unique string.
```

### Client

```shell
$ aac client create [--client-id <client_id>]  # create and switch to client. The <client_id> would be printed and stored in $AAC_CLIENT_ID
acc client list-user [--verbose]               # list all users that can be accessed
```

### User

```shell
aac user create --user <username> --key <key> --client <client_id>  # create a user with name:<username> and key:<key> in client:<client_id>
aac user login --user <username> --key <key> --client <client_id> # set AAC_USER as <username> in client:<client_id>
aac logout                               # clear AAC_USER
```

### NFT

```shell
acc nft create [--user <username>] [--name <name>] [--symbol <symbol>] [--total <total>] [--url <url>] [--description <description>] [--id <nft_id>]
```

### Auction

```shell
aac auction list --current   #
aac auction list             # list all current open auctions with current bid
aac auction list -all        #
aac auction list -a          # list all auctions with last bid
aac auction create --nft <nft_id> [--start <start_time>] [--end <end_time>] [--price <price>] [--client <client_id>]       # create an auction
```

#### Auction actions

- All commands in this chapter requires AAC_USER.
- All commands in this chapter use AAC_AUCTION_ID if no flag --auction-id is offered.
- Auction should be open to interact with, otherwise will return an error.

```shell
aac new <auction_info>          # ??? new user? new client? new auction?
aac auction new <auction_info>  # create an auction. require AAC_USER
aac bid <str_num>               #
aac auction bid <str_num>       # bid on an auction. require AAC_USER
aac raise <str_num>             #
aac auction raise <str_num>     # bid with <last_bid>+<str_num> on an auction. require AAC_USER
```

## Contribute

There's no contribution guide. You can PR whatever you want.

### Todo

- [ ] Use Docker
- [ ] Write tests
- [ ] Write example like [algorand/auction-demo](https://github.com/algorand/auction-demo).
- [ ] Running index will show help then ask for example
- [ ] Web GUI to show API usage

#### example

Output from [algorand dev portal](https://developer.algorand.org/docs/get-started/dapps/pyteal/#setup-environment-and-run-tests)

```
#output
Alice is generating temporary accounts...
Alice is generating an example NFT...
The NFT ID is: 17
Alice is creating auction smart contract that lasts 30 seconds to auction off NFT...
Alice is setting up and funding NFT auction...
Alice's algo balance:  99998100  algos
The smart contract now holds the following: {0: 202000, 17: 1}
Carla wants to bid on NFT, her algo balance:  100000100  algos
Carla is placing bid for:  1000000  algos
Carla is opting into NFT with id: 17
Alice is closing out the auction....
The smart contract now holds the following: {0: 0}
Carla's NFT balance: 1  for NFT ID:  17
Alice's balances after auction:  {0: 101197100, 17: 0}  Algos
Carla's balances after auction:  {0: 98997100, 17: 1}  Algos
```

Ideal Output

```
#output
[Alice ]   Generating temporary accounts...
[Alice ]   Generating an example NFT...
[Client]   The NFT ID is: 17
[Alice ]   Creating auction smart contract that lasts 30 seconds to auction off NFT...
[Alice ]   Setting up and funding NFT auction...
[Alice ]   algo balance:  99998100  algos
[Client]   The smart contract now holds the following: {0: 202000, 17: 1}
[Bob   ]   wants to bid on NFT, with algo balance:  100000100  algos
[Bob   ]   placing bid for:  1000000  algos
[Bob   ]   opting into NFT with id: 17
[Alice ]   Closing out the auction....
[Client]   The smart contract now holds the following: {0: 0}
[Bob   ]   NFT balance: 1  for NFT ID:  17
[Alice ]   balances after auction:  {0: 101197100, 17: 0}  Algos
[Bob   ]   balances after auction:  {0: 98997100, 17: 1}  Algos
```

Ideal CLI to run:

```shell
aac client create
aac nft create --user CLIENT --id:0 --total 202000 # get balance for smart contract CLIENT
aac user create --user Alice
aac nft create --user Alice --id:0 --total 99998100 # get balance for smart contract CLIENT
aac user create --user Bob
aac nft create --user Bob --id:0 --total 100000100 # get balance for smart contract CLIENT
aac user login --user Alice
aac nft create --user Alice | $nft_id # create a new NFT under name of Alice
## or how to use the nft_id from the previous command
aac auction create --nft $nft_id --start "now" --end "+30s" --price 1000000
aac bid --user Bob 1000000 # aac bid --user Bob 1000k # aac bid --user Bob 1M
acc client list-user --verbose --all
```
