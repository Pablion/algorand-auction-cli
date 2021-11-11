# algorand-auction-cli

An interactive NodeJS CLI version of algorand auction-demo repo with Typescript. Also a byproduct of personal studying.
Link: [algorand/auction-demo](https://github.com/algorand/auction-demo).

## Install

Do `yarn install` then `yarn build`.
This package will add two CLI commands: `algorand-auction-cli` and `algorand`

### Trouble shooting

- [Permission denied for package after using yarn link](https://github.com/yarnpkg/yarn/issues/3587)

## CLI usage example

### Var

```shell
$AA_USER          # username of current user
$AA_AUCTION_ID    # auction id of current auction
```

### Type and class

```shell
<str_num>      # parse 20k; 20m; 200_000; 2,000;
<auction_info> # auction info like start time and end time etc.
```

### User

```shell
aa sign --user <username> --key <key>   # create a user with name:<username> and key:<key>
aa login --user <username> --key <key>  # set AA_USER as <username>
aa logout                               # clear AA_USER
```

### Auction

```shell
aa list --current   #
aa list             # list all current open auctions with current bid
aa list -all        #
aa list -a          # list all auctions with last bid
```

#### Auction actions

- All commands in this chapter requires AA_USER.
- All commands in this chapter use AA_AUCTION_ID if no flag --auction-id is offered.
- Auction should be open to interact with, otherwise will return an error.

```shell
aa new <auction_info>          #
aa auction new <auction_info>  # create an auction. require AA_USER
aa bid <str_num>               #
aa auction bid <str_num>       # bid on an auction. require AA_USER
aa raise <str_num>             #
aa auction raise <str_num>     # bid with <last_bid>+<str_num> on an auction. require AA_USER
```

## Contribute

There's no contribution guide. You can PR whatever you want.
