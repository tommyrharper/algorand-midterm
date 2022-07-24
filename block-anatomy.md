# Block Anatomy

At a high level (as described in the whitepaper), a block B$^{r}$ in Algorand can be described as follows:

B$^{r}$ = ( r, PAY$^{r}$, Q$^{r}$, H(B$^{r-1}$), CERT$^{r}$ )

- r - The round number.
- PAY$^{r}$ - The set of payments for that round.
- Q$^{r}$ - The Quantity Seed - a provably unpredictable and not influentiable quantity, used to derive via Cryptographic Sortition the leader for each block and the committee members for each round.
- H(B$^{r}$) - The hash of the previous block.
- CERT$^{r}$ - The block certificate provided by the set of voters or the committee.

In Algorand's official implementation however, within a block you will see the following components:

- `Hash` - A hash for the current block.
- `PreviousBlockHash` - A hash of the previous block.
- `Seed` - The sortition seed.
- `Proposer` - The public key/address of the block proposer.
- `Round` - The round number.
- `Period` - The period in which a block is confirmed. In Algorand the Rewards Period defines the number of Blocks between per Block reward calculations. During a given period block rewards are constant. Then at the beginning of a new period, rewards per block are recalculated.
- `TransactionsRoot` - This is defined as the root of a merkle tree whose leaves are the block's transaction ids, in lexicographic order. For an empty block this is zero.
- `RewardsLevel` - Specifies how many rewards in MicroAlgos have been given to each "RewardUnit" since genesis. The RewardUnit is the minimum amount of Algo that can earn a staking reward. 
- `RewardsRate` - The number of new MicroAlgos added to the participation stake from rewards at the next round.
- `RewardsResidue` - The number of leftover MicroAlgos after the distribution of the RewardsRate MicroAlgos for every "RewardUnit" in the next round.
- `Transactions` - A list of all the transactions in a block.
- `Timestamp` - A timestamp in seconds since the epoch of Algorand.
- `CompactCertVoters` - The root of the merkle tree for which the leaves are all voters who formed part of the committee for this block.
- `CompactCertVotersTotal` - The total amount of MicroAlgos staked by the votes in the CompactCertVoters merkle tree.
- `CompactCertNextRound` - The next round for which a compact certificate is expected. Compact certificates are a certificate than can convince verifiers that signers with a sufficient total weight signed without seeing or verifying all the individual signatures. This is used to demonstrate that parties with a sufficient total Algo balance have attested to the validity of a given block in Algorand.

