# Justcli Document



Justcli is the client of JUST Chain. Users can complete a series of operations on JUST Chain through this client. The following features will be included in version 1.0:

- Create new account
- Generate mnemonics
- Export and import privatekey
- Delete and update accounts
- Transfer and accept JT
- Check account balance
- Participate in PoS mining
- Query and get mining rewards
- View total JT supply
- View basic network conditions
- JUST Chain node configuration



In later versions, Justcli will continue to add various modules and functions according to the white paper, and gradually realize the functions planned on the white paper.




# Installation 

### Runtime Environment

Support linux operating system, ubuntu 16+, centOS 7+ are recommended



### Install justcli
Download the execution file of justcli, copy it to the / usr / local / bin directory, and enter the directory to modify the execution permissions
```
chmod 777 justcli
```


Run the `justcli -h`, if the following is displayed, the installation was successful

```shell
Command line interface for interacting with justd

Usage:
  justcli [command]

Available Commands:
  status      Query remote node for status
  config      Create or query an application CLI configuration file
  query       Querying subcommands
  tx          Transactions subcommands
              
              
  keys        Add or view local private keys
              
  help        Help about any command

Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
  -h, --help              help for justcli
      --home string       directory for config and data (default "/root/.justcli")
  -o, --output string     Output format (text|json) (default "text")
      --trace             print out full stack trace on errors

Additional help topics:
  justcli                       

Use "justcli [command] --help" for more information about a command.
```





### Setting up justcli

First, set up the address of the full-node (node.justuni.club:26650) you want to connect to:
```
justcli config node <host>:<port>
# example: justcli config node tcp://your.trusted.node.address:port
```
Then, let us set the default value of the --trust-node flag:
```
justcli config trust-node true
```
Finally, let us set the chain-id of the blockchain we want to interact with:
```
justcli config chain-id justnet
```
Run "justcli status"，returning node parameters indicates a successful connection
```
justcli status
```







### Generate Keys

You'll need an account private and public key pair (a.k.a. sk, pk respectively) to be able to receive funds, send txs, lock tx, etc.

To generate a new secp256k1 key:
```
justcli keys add <account_name>
```
Next, you will have to create a passphrase to protect the key on disk. The output of the above command will contain a seed phrase. It is recommended to save the seed phrase in a safe place so that in case you forget the password, you could eventually regenerate the key from the seed phrase with the following command:
```
justcli keys add <account_name> -i
```
You can see all your available keys by typing:
```
justcli keys list
```
After receiving JT to your address, you can view your account's balance by typing:
```
justcli query account <account_address>
```
> Warning Note: When you query an account balance with zero JT, you will get this error: No account with address <account_cosmos> was found in the state. This can also happen if you fund the account before your node has fully synced with the chain. These are both normal.

### Send JT
The following command could be used to send coins from one account to another:
```
justcli tx send <account_name> <receive_address> 100000000000000000000ajt --fees=5000000000000000ajt
```
> 1jt=10^18ajt。fees：5000000000000000ajt，above is a sample of transfering 100jt

### Staking
On the Just mainnet, we delegate ajt, where 1jt = 10^18ajt. You can query the list of all supernodes of a specific chain:
```
justcli query staking validators
```
 Here's how you can lock JT to a supernodes:
```
justcli tx staking delegate <supernodes_address> <amount>ajt --from <account_name> --fees=5000000000000000ajt
```
Once submitted a delegation to a supernode, you can see it's information by using the following command:
```
justcli query staking delegation <delegator_address> <supernode_address>
```
If you want to check all your current delegations with disctinct supernodes:
```
justcli query distribution rewards <account_address>
```
Withdraw all your profits:
```
justcli tx distribution withdraw-all-rewards --from <account_name> --fees=5000000000000000ajt
```



##### More operations query with `justcli -h`


