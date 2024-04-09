# Last mile transactions

> 💡 Is it possible to use lightning network without the initial funding transaction? \
> *So that on-chain transactions are only used in case of a dispute?*

## What are the requirements?

- Dishonesty must be disadvantageous. Let's try to use the game theory for securing the transfers. 

### Simple example

- Alice owns UTXO with 10 bitcoin
- Alice decides to send 1 bitcoin to Bob

| Transaction outputs | Alice | Bob | Punishment Fee |
| --- | --- | --- | --- |
| Status transaction | 9 | 1 | 0 |

It's a normal transaction that Alice or Bob can broadcast. However, to save on fees, they will keep it with them and delay disclosure.

## Threat Mitigation

### 1. How to prevent Alice from creating another transaction?

*Alice can create another transaction at any time to send the UTXO to anyone else.*

Bob won't be satisfied with a signed transaction with the new status. He'll also want a `defense` transaction. The `defense` transaction will use the identical input as the main transaction (10 BTC) and two outputs. 

| Transaction outputs | Alice | Bob | Punishment Fee |
| --- | --- | --- | --- |
| Defense transaction | 8 | 0.5 | 1.5 |

If Alice creates a fraudulent transaction, Bob can share a `defense` transaction. While he will hurt himself a bit (he will only get 0.5 bitcoin instead of 1), he will also punish Alice, who will only get 8 bitcoin instead of 9. This `defense` transaction will burn most of the funds to pay the miners. This ensures that miners have an incentive to mine this transaction before any other transaction that Alice would have come up with. In theory, Alice could create a higher priority transaction, but she would have to damage herself even more.

Bob has no incentive to use a `defense` transaction unless he is in danger. Because he has fewer resources in it than in a `status` transaction.

→ 🟢 Alice is not motivated to attack since Bob can harm her with `defense` transaction

### 2. How to prevent Alice from making promises to more people?

*Alice can make promise to infinite recipients. But at most one will receive the funds.*

Alice will need to disclose information that a given UTXO is partially pledged to a particular bitcoin address. This information can be shared with nodes that would have the assigned counter addresses in addition to a list of valid UTXOs. Or, for example, Alice can share this information via nostr on generally know relay (or more of them).

Bob will only consider a transaction valid if he sees the information shared by Alice through a standardized channel, and at the same time he does not see a similar binding to any other bitcoin address.

- *If Bob discovers a connection to a another address at any later time, he should immediately post a `defense` transaction.*
- *Using one UTXO for multiple addresses would require more complex coordination.*

→ 🟢 Bob can ensure that Alice is not promising her UTXO to anyone else at the moment

### 3. How to protect Bob against the collaboration of miners?

*Bob may not have time to respond if Alice sends the transaction directly to the miner.*

For miner is economical to mine a `defense` rather than `attack` a transaction. However, it is possible that they will not have access to the `defense` transaction. Miner can communicate proof that he has an `attack` transaction from Alice. So the Bob is motivated to broadcast the `defense` transaction.

Alice can collect the whole fee and mine that transaction. However if she cooperates with mining pool other miners are again motivated to broadcast this transaction and notify potential Bob

→ 🟢 Miner is motivated to publish received transaction to notify potential Bob

### 4. How to prevent the long-term collaboration with miners?

*Bob can share the `defense` transaction with mining pool under condition that they will share part of the punishment fee.*

For example half of the reward:

| Transaction outputs | Alice | Bob | Punishment Fee |
| --- | --- | --- | --- |
| Defense transaction | 8 | 0.5 (+0,75) | 1.5 (-0,75) |

Alice can similarly bribe miners (sharing valuable transaction with conditions and long-term cooperation). In another words, miners could get more if they don’t collaborate but not in repeated game. On the other hand they will ruin their income in even longer period.

→ 🟠 This problem seems serious to me as of now, but not critical

### 5. How do we make sure Bob doesn't attack even if he has nothing to lose?

If Bob sends all the resources back to Alice, he has nothing to lose, but he can harm her. He can share an old defense transaction that burns some of the resources for the miners.

| Transaction outputs | Alice | Bob | Punishment Fee |
| --- | --- | --- | --- |
| Status transaction | 10 | 0 | 0 |
| Old Defense transaction | 8 | 0.5 | 1.5 |

→ 🟡 Bob’s balance should go to zero or the UTXO should be updated. This is quite limiting and this prevents the effective use of one utxo for multiple people. 

**An option to set the transaction expiration would solve the problem.**

## Transaction Expiration

Bitcoin transaction may contain a `Locktime`, which determines the point at which the transaction is `final` and can be broadcasted and mined.

To be able to securely reuse UTXO without on-chain transaction, we need to be able to cancel the promise. Invalidate the transaction after a certain period of time. A transaction that had a specified expiration block size could not be mined after the block had expired - such transaction wouldn’t be valid anymore. 

→ 🔴 Bitcoin soft-fork is required to unleash full potential of Last Mile

## Potential impact of `Last Mile`

### Scaling

- Self-custody without costs for as many users as there are currently UTXOs. 
*In 2024 more than 170M.*
    - The given UTXO must be at least 3 times larger than dust to pay the lowest mining fee, to create at least a dust UTXO for Bob and to protect against Alice's attack. Ideally it should be bigger, but it doesn't have to be huge. But for the sake of simplicity, let's say that UTXO must not be less than 2000 sats.
- UTXO does not have to be actually spent → The channel can stay open or be closed either in the intermediate state or the whole UTXO is sent to Alice or Bob
    - There is workaround with introduction of other risk. Clean solution would be to introduce `Expiration` into bitcoin.
- Last Mile could be connected with Lightning Network if Alice has some lightning channels.
- Status transactions could be coordinated into coinjoin to save even more on fees

### Decentralization

- More people can became self-sovereign - without relying on service providers

### Fees

- There is still a need to record transactions if one wants to be sure
- Owners of multiple UTXOs can provide routing similar to LN

## Visualisation for better understanding
**Simple existence of bitcoin users** \
Dots are emerging and dissapearing when users are doing transactions on-chain.
![LM schema 1](https://github.com/hynek-jina/Hynek/assets/26002916/03237b59-c2b4-4cdb-802e-26b2562e083d)

**Introduction of Lightning Network** \
Lightning is clearing the state between two parties and connects to the the network.
![LM schema 2](https://github.com/hynek-jina/Hynek/assets/26002916/1f00ea20-b5fe-439d-9a4d-189f5df1b466)

**Last mile ambition** \
Last mile could anable more people to have real but unconfirmed bitcoin and manipulate with it according their need.
![LM schema 3](https://github.com/hynek-jina/Hynek/assets/26002916/ff5f99a8-e7cd-456d-8240-c087308ee072)

### Last mile offers another trade-off between security and costs
![LM comparison](https://github.com/hynek-jina/Hynek/assets/26002916/b015b204-7890-40c4-81cc-c1824d967167)

## Summary

- 🟢 Regular bitcoin addresses can be used
- 🟢 Anyone could accept bitcoin and being connected to Lightning Network non-custodial way without need of opening channel fee
- 🟢 Immediate transactions
- 🟢 There could be multiple users in a single UTXO channel
- ⚪ Multiple UTXO owners can route payments
- ⚪ Could be connected to Lightning
- ⚪ Up to half the size of the UTXO can be used in one channel
- ⚪ Might be more useful for relatively smaller UTXOs
- 🟡 All participants must be online to update the transactions
- 🟡 Risk that the counterparty gets nervous and you both lose part of the funds
- 🟡 Risk that the counterparty is also a huge individual miner and can steal some funds (in case of receiver) or even all the funds (in case o UTXO owner/initial sender)
- 🟠 Risk of long-term collaboration with miners

With activation of transaction `Expiration`:

- 🟢 UTXO can be endlessly reused
