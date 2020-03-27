# Vote

### Governance

Governance is the process from which users in the JustNet can come to consensus on software upgrades, parameters of the mainnet or signaling mechanisms through text proposals. This is done through voting on proposals, which will be submitted by `JT` holders on the mainnet.

Some considerations about the voting process:

- Voting is done by bonded `JT` holders on a 1 bonded `JT` 1 vote basis
- Delegators inherit the vote of their Supernode if they don't vote
- Votes are tallied at the end of the voting period (2 days) where each address can vote multiple times to update its `Option` value (paying the transaction fee each time), only the most recently cast vote will count as valid
- Voters can choose between options `Yes`, `No`, `NoWithVeto` and `Abstain`
- At the end of the voting period, a proposal is accepted if:
  - `(YesVotes / (YesVotes+NoVotes+NoWithVetoVotes)) > 1/2`
  - `(NoWithVetoVotes / (YesVotes+NoVotes+NoWithVetoVotes)) < 1/3`
  - `((YesVotes+NoVotes+NoWithVetoVotes) / totalBondedStake) >= quorum`
  
### Who can vote

On the JustNet, participants are bonded JT holders. Unbonded JT holders and other users do not get the right to participate in governance.

### Voting period

We define `Voting period` as the interval between the moment the vote opens and the moment the vote closes. The initial value of `Voting period` is 48 hours.

### Option set

The option set of a proposal refers to the set of choices a participant can choose from when casting its vote.

The initial option set includes the following options: 
- `Yes`
- `No`
- `NoWithVeto` 
- `Abstain` 

`NoWithVeto` counts as `No` but also adds a `Veto` vote. `Abstain` allows voters to signal that they do not intend to vote in favor or against the proposal but accept the result of the vote. 

### Quorum 

Quorum is defined as the minimum percentage of voting power that needs to be casted on a proposal for the result to be valid. The initial value of `Quorum` is 1/3.

### Threshold

Threshold is defined as the minimum ratio of `Yes` votes to `No` votes for the proposal to be accepted.

Initially, the threshold is set at 50% with a possibility to veto if more than 1/3rd of votes (excluding `Abstain` votes) are `NoWithVeto` votes. This means that proposals are accepted is the ratio of `Yes` votes to `No` votes at the end of the voting period is superior to 50% and if the number of `NoWithVeto` votes is inferior to 1/3rd of total votes (excluding `Abstain`).

`Urgent` proposals also work with the aforementioned threshold, except there is another condition that can accelerate the acceptance of the proposal. Namely, if the ratio of `Yes` votes to `InitTotalVotingPower` exceeds 2/3, `UrgentProposal` will be immediately accepted, even if the `Voting period` is not finished. `InitTotalVotingPower` is the total voting power of all bonded JT holders at the moment when the vote opens.

### Inheritance

If a delegator does not vote, it will inherit its Supernode vote.

- If the delegator votes before its Supernode, it will not inherit from the Supernode's vote.
- If the delegator votes after its Supernode, it will override its Supernode vote with its own vote.

### Command
Query information of the proposal
```
justcli query gov proposal <proposal_id>
```
Vote on a Proposal
```
justcli tx gov vote <proposal_id> <Yes/No/NoWithVeto/Abstain> --from=<account_name> --fees=5000000000000000ajt
```
Check the vote with the option you just submitted
```
justcli query gov vote <proposal_id> <voter_address>
```
You can also get all the previous votes submitted to the proposal with
```
justcli query gov votes <proposal_id>
```
To check the current tally of a given proposal you can use the tally command:
```
justcli query gov tally <proposal_id>
```
