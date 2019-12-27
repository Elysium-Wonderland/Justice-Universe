# Justcli Keys command



Keys allows you to manage your local keystore. These keys may be in any format supported by go-crypto and can be used by light-clients, full nodes, or any other application that needs to sign with a private key.



### Keys Command List

- mnemonic
  - Compute the bip39 mnemonic for some input entropy
- add 
  - Add an encrypted private key (either newly generated or recovered), encrypt it, and save to disk
- export
  - Export private keys
- import
  - Import private keys into the local keybase
- list
  - List all keys
- show
  - Show key info for the given name
- delete
  - Delete the given key
- update
  - Change the password used to protect private key
- parse
  - Parse address from hex to bech32 and vice versa



```
justcli keys -h



Usage:
  justcli keys [command]

Available Commands:
  mnemonic    Compute the bip39 mnemonic for some input entropy
  add         Add an encrypted private key (either newly generated or recovered), encrypt it, and save to disk
  export      Export private keys
  import      Import private keys into the local keybase
  list        List all keys
  show        Show key info for the given name
              
  delete      Delete the given key
  update      Change the password used to protect private key
  parse       Parse address from hex to bech32 and vice versa

Flags:
  -h, --help   help for keys

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
      --home string       directory for config and data (default "/root/.justcli")
  -o, --output string     Output format (text|json) (default "text")
      --trace             print out full stack trace on errors

Use "justcli keys [command] --help" for more information about a command.
```



### Mnemonic subcommand



```
justcli keys mnemonic -h

Create a bip39 mnemonic, sometimes called a seed phrase, by reading from the system entropy. To pass your own entropy, use --unsafe-entropy

Usage:
  justcli keys mnemonic [flags]

Flags:
  -h, --help             help for mnemonic
      --unsafe-entropy   Prompt the user to supply their own entropy, instead of relying on the system

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
      --home string       directory for config and data (default "/root/.justcli")
  -o, --output string     Output format (text|json) (default "text")
      --trace             print out full stack trace on errors
```



##### Example

export the bip39 mnemonic



```shell
justcli keys mnemonic


balance torch xxx xxx xxxx xxxx xxxx xxxx xxxx xxxxx xxxxx xxxx xxxxx xxxxx xxxxx hip record produce any earn
```



### justcli keys add subcommand



Derive a new private key and encrypt to disk.

Optionally specify a BIP39 mnemonic, a BIP39 passphrase to further secure the mnemonic,

and a bip32 HD path to derive a specific account. The key will be stored under the given name

and encrypted with the given password. The only input that is required is the encryption password.



If run with -i, it will prompt the user for BIP44 path, BIP39 mnemonic, and passphrase.

The flag --recover allows one to recover a key from a seed passphrase.

If run with --dry-run, a key would be generated (or recovered) but not stored to the

local keystore.

Use the --pubkey flag to add arbitrary public keys to the keystore for constructing

multisig transactions.



You can add a multisig key by passing the list of key names you want the public

key to be composed of to the --multisig flag and the minimum number of signatures

required through --multisig-threshold. The keys are sorted by address, unless

the flag --nosort is set.



```
justcli keys add -h


Usage:
  justcli keys add <name> [flags]

Flags:
      --account uint32            Account number for HD derivation
      --dry-run                   Perform action, but don't add key to local keystore
  -h, --help                      help for add
      --indent                    Add indent to JSON response
      --index uint32              Address index number for HD derivation
  -i, --interactive               Interactively prompt user for BIP39 passphrase and mnemonic
      --ledger                    Store a local reference to a private key on a Ledger device
      --multisig strings          Construct and store a multisig public key (implies --pubkey)
      --multisig-threshold uint   K out of N required signatures. For use in conjunction with --multisig (default 1)
      --no-backup                 Don't print out seed phrase (if others are watching the terminal)
      --nosort                    Keys passed to --multisig are taken in the order they're supplied
      --pubkey string             Parse a public key in bech32 format and save it to disk
      --recover                   Provide seed phrase to recover existing key instead of creating

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
      --home string       directory for config and data (default "/root/.justcli")
  -o, --output string     Output format (text|json) (default "text")
      --trace             print out full stack trace on errors
```



##### Example

Derive a new private key and encrypt to disk.



```shell
justcli keys add abc


Enter a passphrase to encrypt your key to disk:
Repeat the passphrase:

- name: abc
  type: local
  address: jt1hammw8h4tu693y67mwxauyqktlzrd72ezj4xhy
  pubkey: jtpub1addwnpepqwv6hphpdd6yd4jphh4t6kuuu29jdma57xzqag99444z2dvx223yu9gxzup
  mnemonic: ""
  threshold: 0
  pubkeys: []


**Important** write this mnemonic phrase in a safe place.
It is the only way to recover your account if you ever forget your password.

drift tunnel xxxx xxxxx xxxxx xxxxx xxxxx xxxxx xxxxx xxxxx xxxxx xxxxx xxxxx xxxxx xxxxx xxxxx xxxxx xxxxx xxxxx xxxxx xxxxx medal repeat
```



### justcli keys export subcommand

Export a private key from the local keybase in ASCII-armored encrypted format.



```shell
justcli keys export -h


Usage:
  justcli keys export <name> [flags]

Flags:
  -h, --help   help for export

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
      --home string       directory for config and data (default "/root/.justcli")
  -o, --output string     Output format (text|json) (default "text")
      --trace             print out full stack trace on errors
```



### justcli keys import subcommand

Import a ASCII armored private key into the local keybase.

```shell
justcli keys import -h


Usage:
  justcli keys import <name> <keyfile> [flags]

Flags:
  -h, --help   help for import

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
      --home string       directory for config and data (default "/root/.justcli")
  -o, --output string     Output format (text|json) (default "text")
      --trace             print out full stack trace on errors
```





### justcli keys list subcommand

Return a list of all public keys stored by this key manager along with their associated name and address.



```shell
justcli keys list -h


Usage:
  justcli keys list [flags]

Flags:
  -h, --help     help for list
      --indent   Add indent to JSON response

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
      --home string       directory for config and data (default "/root/.justcli")
  -o, --output string     Output format (text|json) (default "text")
      --trace             print out full stack trace on errors


```



##### Example:

```
justcli keys list

- name: abc
  type: local
  address: jt1hammw8h4tu...........d72ezj4xhy
  pubkey: jtpub1addwnpepqwv6h...............99444z2dvx223yu9gxzup
  mnemonic: ""
  threshold: 0
  pubkeys: []

```



### justcli keys show subcommand

Return public details of a single local key. If multiple names are provided, then an ephemeral multisig key will be created under the name "multi" consisting of all the keys provided by name and multisig threshold.



```shell
justcli keys show -h


Usage:
  justcli keys show [name [name...]] [flags]

Flags:
  -a, --address                   Output the address only (overrides --output)
      --bech string               The Bech32 prefix encoding for a key (acc|val|cons) (default "acc")
  -d, --device                    Output the address in a ledger device
  -h, --help                      help for show
      --indent                    Add indent to JSON response
      --multisig-threshold uint   K out of N required signatures (default 1)
  -p, --pubkey                    Output the public key only (overrides --output)

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
      --home string       directory for config and data (default "/root/.justcli")
  -o, --output string     Output format (text|json) (default "text")
      --trace             print out full stack trace on errors
```



##### Example:

show details of the account



```
justcli keys show abc

- name: abc
  type: local
  address: jt1hamm.....................zj4xhy
  pubkey: jtpub1ad...............................................23yu9gxzup
  mnemonic: ""
  threshold: 0
  pubkeys: []
```



### justcli keys delete subcommand



Delete a key from the store.



```shell
justcli keys delete -h


Usage:
  justcli keys delete <name> [flags]

Flags:
  -f, --force   Remove the key unconditionally without asking for the passphrase
  -h, --help    help for delete
  -y, --yes     Skip confirmation prompt when deleting offline or ledger key references

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
      --home string       directory for config and data (default "/root/.justcli")
  -o, --output string     Output format (text|json) (default "text")
      --trace             print out full stack trace on errors
```



### justcli keys update subcommand



Change the password used to protect private key



```
justcli keys update -h

Usage:
  justcli keys update <name> [flags]

Flags:
  -h, --help   help for update

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
      --home string       directory for config and data (default "/root/.justcli")
  -o, --output string     Output format (text|json) (default "text")
      --trace             print out full stack trace on errors
```



### justcli keys parse subcommand



```
justcli keys parse -h


Usage:
  justcli keys parse <hex-or-bech32-address> [flags]

Flags:
  -h, --help     help for parse
      --indent   Indent JSON output

Global Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
      --home string       directory for config and data (default "/root/.justcli")
  -o, --output string     Output format (text|json) (default "text")
      --trace             print out full stack trace on errors

```



