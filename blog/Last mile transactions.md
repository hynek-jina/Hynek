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

---

*Other optional steps:*

- *Alice can send Bob additional funds (up to one half the size of the original UTXO in total)*
- *Bob can send the funds back to Alice*
- *Maybe Bob could pay other people via LN if Bob has open channels*

## Summary

- 🟢 Regular bitcoin addresses can be used
- 🟢 Annyone could accept bitcoin and being connected to Lightning Network non-custodial way without necesity of opening channel fee
- 🟢 Immediate transactions
- 🟢 There can be multiple users in a single UTXO channel
- ⚪ Up to half the size of the UTXO can be used in one channel
- ⚪ Might be more useful for relatively smaller UTXOs
- 🟡 All participants must be online to update the transactions
- 🟡 Risk that the counterparty gets nervous and you both lose part of the funds
- 🟡 Risk that the counterparty is also a huge individual miner and can steal some funds (in case of receiver) or even all the funds (in case o UTXO owner/initial sender)
- 🟠 Risk of long-term collaboration with miners
