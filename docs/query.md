# Justcli query command



### Query Command List:

- Account : Query account balance
- Supply       Querying commands for the supply module
- staking      Querying commands for the staking module
- distribution Querying commands for the distribution module

```shell
Querying subcommands

Usage:
  justcli query [command]

Aliases:
  query, q

Available Commands:
  account      Query account balance            
  supply       Querying commands for the supply module
  staking      Querying commands for the staking module
  distribution Querying commands for the distribution module
               

Flags:
  -h, --help   help for query

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
      --home string       directory for config and data (default "/root/.justcli")
  -o, --output string     Output format (text|json) (default "text")
      --trace             print out full stack trace on errors

```



### Justcli query account



```shell
justcli query account -h

Query account balance

Usage:
  justcli query account [address] [flags]

Flags:
      --height int    Use a specific height to query state at (this can error if the node is pruning state)
  -h, --help          help for account
      --indent        Add indent to JSON response
      --ledger        Use a connected Ledger device
      --node string   <host>:<port> to Tendermint RPC interface for this chain (default "tcp://localhost:26657")
      --trust-node    Trust connected full node (don't verify proofs for responses)

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
      --home string       directory for config and data (default "/root/.justcli")
  -o, --output string     Output format (text|json) (default "text")
      --trace             print out full stack trace on errors
```



##### Query the balance of an address

`justcli query account [address]`

e.g: 

```
justcli query account jt1ggsgqj3r3esdq0gy2q8cst4epc0ru7klhkhfg2

  address: jt1ggsgqj3r3esdq0gy2q8cst4epc0ru7klhkhfg2
  coins:
  - denom: ajt
    amount: "9990000000000000000"
  pubkey: ""
  accountnumber: 4299
  sequence: 0

```



### Justcli Query Supply

Querying commands for the supply module



```shell

justcli query supply -h


Querying commands for the supply module

Usage:
  justcli query supply [flags]
  justcli query supply [command]

Available Commands:
  total       Query the total supply of coins of the chain

Flags:
  -h, --help   help for supply

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
      --home string       directory for config and data (default "/root/.justcli")
  -o, --output string     Output format (text|json) (default "text")
      --trace             print out full stack trace on errors

Use "justcli query supply [command] --help" for more information about a command.
```



##### Example：

```
justcli query supply total


- denom: ajt
  amount: "66674426000000000000000000"
```



### Justcli Query Staking

Querying commands for the staking module



```shell
justcli query staking -h


Querying commands for the staking module

Usage:
  justcli query staking [flags]
  justcli query staking [command]

Available Commands:
  delegation                 Query a delegation based on address and supernode address
  delegations                Query all delegations made by one delegator
  unbonding-delegation       Query an unbonding-delegation record based on delegator and supernode address
  unbonding-delegations      Query all unbonding-delegations records for one delegator
  redelegation               Query a redelegation record based on delegator and a source and destination supernode address
  redelegations              Query all redelegations records for one delegator
  validator                  Query a supernode
  validators                 Query for all supernodes
  delegations-to             Query all delegations made to one supernode
  unbonding-delegations-from Query all unbonding delegatations from a supernode
  redelegations-from         Query all outgoing redelegatations from a supernode
  params                     Query the current staking parameters information
  pool                       Query the current staking pool values

Flags:
  -h, --help   help for staking

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
      --home string       directory for config and data (default "/root/.justcli")
  -o, --output string     Output format (text|json) (default "text")
      --trace             print out full stack trace on errors

Use "justcli query staking [command] --help" for more information about a command.

```



##### Examples1 Get Supernodes Inforamtion:

Get All Supernodes Staking Information

```
justcli query staking supernodes

- |
  operatoraddress: jtvaloper1vkkh5pe5ljalehl7m4zpyj2cjjcdpyphvazr34
  conspubkey: jtvalconspub1zcjduepq5wp0mzyq5khj50rzr96qzjvtjahrf0xrk9xys8tz0asgsccurpgsrxktsq
  jailed: false
  status: 2
  tokens: "1000000000000000000000000"
  delegatorshares: "1000000000000000000000000.000000000000000000"
  description:
    moniker: justGenesis
    identity: ""
    website: ""
    details: ""
  unbondingheight: 0
  unbondingcompletiontime: 1970-01-01T00:00:00Z
  commission:
    commission_rates:
      rate: "0.050000000000000000"
      max_rate: "0.200000000000000000"
      max_change_rate: "0.010000000000000000"
    update_time: 2019-12-26T09:53:23.175574973Z
  minselfdelegation: "10000000000000000000000"
- |

```



##### Examples2: Get Staking Information

```
justcli query staking params

unbonding_time: 336h0m0s
max_validators: 100
max_entries: 7
bond_denom: ajt
min_self_delegation: "10000000000000000000000"
```



### Justcli Query Distribution



Querying commands for the distribution module

```
justcli query distribution -h


Querying commands for the distribution module

Usage:
  justcli query distribution [flags]
  justcli query distribution [command]

Available Commands:
  params                        Query distribution params
  validator-outstanding-rewards Query distribution outstanding (un-withdrawn) rewards for a supernode and all their delegations
  commission                    Query distribution supernode commission
  slashes                       Query distribution supernode slashes
  rewards                       Query all distribution delegator rewards or rewards from a particular supernode
  community-pool                Query the amount of coins in the community pool

Flags:
  -h, --help   help for distribution

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
      --home string       directory for config and data (default "/root/.justcli")
  -o, --output string     Output format (text|json) (default "text")
      --trace             print out full stack trace on errors

Use "justcli query distribution [command] --help" for more information about a command.
```



