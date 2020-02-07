# Supernode

### What is a full-node?
A full-node is a program that fully validates transactions and blocks of a blockchain. It is distinct from a light-node that only processes block headers and a small subset of transactions. Running a full-node requires more resources than a light-node but is necessary in order to be a supernode. In practice, running a full-node only implies running a non-compromised and up-to-date version of the software with low network latency and without downtime.

Of course, it is possible and encouraged for users to run full-nodes even if they do not plan to be supernodes.

### How to become a supernode?
Any participant in the network can signal that they want to become a supernode by sending a create-validator transaction, where they must fill out the following parameters:

Supernode's PubKey: The private key associated with this Tendermint PubKey is used to sign prevotes and precommits. 

Supernode's Address: Application level address. This is the address used to identify your supernode publicly. The private key associated with this address is used to delegate, unbond, claim rewards, and participate in governance.
Supernode's name (moniker)
Supernode's website (Optional)
Supernode's description (Optional)

Initial commission rate: The commission rate on block rewards and fees charged to delegators.

Maximum commission: The maximum commission rate which this supernode can charge. This parameter cannot be changed after create-validator is processed.

Commission max change rate: The maximum daily increase of the supernode  commission. This parameter cannot be changed after create-validator is processed.

Minimum self-delegation: Minimum amount of JT the supernode needs to have bonded at all time. If the supernode's self-delegated stake falls below this limit, their entire staking pool will unbond.

Once a supernode is created, JT holders can delegate JT to them, effectively adding stake to their pool. The total stake of an address is the combination of JT bonded by delegators and JT self-bonded by the entity which designated themselves.

Out of all supernode candidates that signaled themselves, the 100 with the most total stake are the ones who are designated as supernodes. They become supernodes If a supernode's total stake falls below the top 100 then that supernode loses their supernode privileges: they don't participate in consensus and generate rewards any more.

## Join the Just Net

### Install justd & justcli
justcli need update to the version V1.1
```
wget https://github.com/Elysium-Wonderland/Justice-Universe/releases/download/V1.1/justd.tar.gz
wget https://github.com/Elysium-Wonderland/Justice-Universe/releases/download/V1.1/justcli.tar.gz
```
copy justd & justcli to the / usr / local / bin directory, and enter the directory to modify the execution permissions
```
chmod 777 justd
chmod 777 justcli
```

### Set a full-node
initialize network
```
justd init <your_moniker> --chain-id justnet
```
overwrite ~/.justd/config/genesis.json with just net's genesis.json, you can get the json file like
```
curl https://raw.githubusercontent.com/Elysium-Wonderland/Justice-Universe/master/genesis.json > $HOME/.justd/config/genesis.json
```
modify the ~/.justd/config/config.toml, change the persistent_peers config
```
persistent_peers = "196b4202bb19690808f6e8f6a08464454c949d46@165.227.189.246:26656,9ac993102af9256dc44d9bb3e2e6d59bd8bbef66@157.245.215.213:26656,f3151e9e52dfe96788def701016f017dbb8189be@47.244.49.18"
```
set the gasprice and start
```
nohup justd start --minimum-gas-prices 25000000000.0ajt > jd.log &
```

### Set a supdernode
Your jtvalconspub can be used to create a new supernode by staking tokens. You can find your supernode pubkey by running:
```
justd tendermint show-validator
```
To set your supernode, your full-node should synchronize to the latest block, then use the following command:
```
justcli tx staking create-validator \
--amount=10000000000000000000000ajt \
--pubkey=$(justd tendermint show-validator) \
--moniker="<your_moniker>" \
--chain-id=justnet \
--commission-rate="0.05" \
--commission-max-rate="0.20" \
--commission-max-change-rate="0.01" \
--min-self-delegation="10000000000000000000000" \
--from=<account_name> \
--fees=5000000000000000ajt
```

### Edit Supernode Description
You can edit your supernode's public description. This info is to identify your supernode, and will be relied on by delegators to decide which supernode to stake to. Make sure to provide input for every flag below. If a flag is not included in the command the field will default to empty (--moniker defaults to the machine name) if the field has never been set or remain the same if it has been set in the past.

The <account_name> specifies which supernode you are editing. If you choose to not include certain flags, remember that the --from flag must be included to identify the supernode to update.

```
justcli tx staking edit-validator \
  --moniker="<your_moniker>" \
  --website="<your_website>" \
  --details="<your_details>" \
  --chain-id="justnet" \
  --gas="auto" \
  --gas-prices="25000000000.0ajt" \
  --gas-adjustment=1.9 \
  --from="<account_name>"
```

### View Supernode Description
View your supernode address
```
justcli keys show <account_name> --bech val
```
example
```
justcli keys show test3 --bech val 
result:
- name: test3
  type: local
  address: jtvaloper1kxh3jwrk2m9a09rd0rl058gjpw3c4h85wy0z9r (here is your supernode address)
  pubkey: jtvaloperpub1addwnpepqgf7qcehhd3hjpnsakj03d8s38gj4uqwhwx8cwl7u7gehj078zh8v2c8q4f
  mnemonic: ""
  threshold: 0
  pubkeys: []
```
View the supernode's information with this command
```
justcli query staking validator <supernode_address>
```
### Withdraw profits and commission
If you want to check all your current delegations with disctinct supernodes
```
justcli query distribution rewards <account_address>
```
Withdraw all your profits
```
justcli tx distribution withdraw-all-rewards --from <account_name> --fees=5000000000000000ajt --broadcast-mode sync
```
If you want to check your current commission
```
justcli query distribution commission <supernode_address>
```
Withdraw your commission
```
justcli tx distribution withdraw-rewards <supernode_address> --from <account_name> --commission --fees=5000000000000000ajt --broadcast-mode sync
```

### Unjail Supernode
Supernodes are responsible for committing new blocks to the blockchain through voting. A supernode's stake is slashed if they become unavailable or sign blocks at the same height. Current slash fraction can be viewed by the command:
```
justcli q slashing params
result:
max_evidence_age: 2m0s
signed_blocks_window: 100
min_signed_per_window: "0.500000000000000000"
downtime_jail_duration: 10m0s
slash_fraction_double_sign: "0.050000000000000000"
slash_fraction_downtime: "0.001000000000000000" (Current slash fraction)
```

When a supernode is "jailed" for downtime, you must submit an Unjail transaction from the operator account in order to be able to get block proposer rewards again (depends on the zone fee distribution).
```
justcli tx slashing unjail --from=<account_name> --fees=5000000000000000ajt
```
