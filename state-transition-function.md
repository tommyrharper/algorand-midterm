# State Transition Function

With the production of each new block the state is updated in the Algorand blockchain.

We notate this as follows:

Round r: S$^{r}$ -> S$^{r+1}$

The round is the block number, and hence S$^{r}$ is the state for that block.

We can describe the state in the block further as follows:

S$^{r}$ = { (i, a$_{i}$ $^{(r)}$, ... ) : i ∈ PK$^{r}$ }

Where i is a particular user, a$_{i}$ $^{(r)}$ is amount for their account and PK$^{r}$ is the set of all public keys with balances for this round.

Hence the state transition function updates for each block the set of public keys PK$^{r}$ stored within the state and their according balances, based on the transactions included in the previous block.

In order to do this, the state transition function must process the payments included in a particular block.

## Payments

Payments are defined as follows:

℘ = SIG$_{i}$(i, i`, a, I, H(I$^{s}$))

Where ℘ the payment is the signature by user i of their public key, the payees public key i`, the amount a, some public information I and the hash of some secret information H(I$^{s}$).

For a particular state transition, the total set of payments is defined as PAY$^{r}$, all the payments for that round.

A given payment ℘ is valid if its amount a is less than or equal to a$_{i}$ $^{r}$ (the amount for that user in that round)
 and it does not appear in any previously finalised payset - PAY$^{r'}$
when r′ < r.

Algorand also says that each payment should specify a round ρ, and that it shall only be valid at any round in the range [ρ, ρ + k] for a non-negative integer k. After this, the payment will be declared invalid must be resubmitted if it has not yet been included in a block.

A payset P (the collection of payments for a given round) is considered valid for a given round if for each user i the payments of i in P (possibly none) are valid and the payset is maximal, meaning that no superset of P is valid.

## Summary

When a new block is proposed, the proposer takes the current state of the system, finds the maximal valid payset, applies all given transactions in said payset and updates the user balances accordingly to generate the new system state.

This is then validated by each committee member before being certified into a new block.
