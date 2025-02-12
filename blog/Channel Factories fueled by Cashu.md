# Channel Factories fueled by Cashu

> *A **purely peer-to-peer** version of electronic cash would allow online payments to be sent directly from one party to another without going through a financial institution.
> ~ Satoshi Nakamoto*


## 🎯 Bitcoin should be for everyone

- On-chain can absorb only cca 17M transactions or channel opens per month which basically limits the maximum number of users that can use bitcoin in full-scope. *- Assuming that you need to change the channel size once a month.*
- We need like 1000x more, or use sidechains, ark, and/or other scaling proposals. *- Each comes with different trade-offs*
- This document is about the idea **How to Enable [Channel Factories](https://bitcoinops.org/en/topics/channel-factories/)** [`CF`]*- group of people can have huge shared utxo with many derived channels and improve these channel without additional on-chain transaction.*

`CF` are complex by themself. I’m not familiar with any solid implementation. But I think that biggest problem with `CF` is not technical, but rather social and incentives related - Just like bitcoin itself.  → It’s quite complicated to organize dozens of users to coordinate the new distribution of the channels at the same time.

## 💫Transactions

Let’s split transactions and the bitcoin settlement. 
*It would be nice to have everything, but on-chain bitcoin doesn’t provide immediate settlement anyway and lightning has another set of limitations.*

### 🫂 Verified Contacts

Bitcoin was designed to be trust-less. However this doesn’t correspond with our society, where trust is very crucial. You don’t benefit much from bitcoin trust-less utility when you transfer money to your best friends. Not everyone is same for you. We still want to achieve the developed network where you can transact trust-less with strangers, but it doesn’t mean we need it everywhere and from the day one. 

The first piece in the puzzle is to distinguish counterparties. Verify the people you trust and be able to specify how much do you trust them.

### 🥜 Cashu Mint

> *If we can’t guarantee that nobody can print money the second best could be that everyone can print. And with verified peers the ecosystem could evolve to intended state that nobody is actually printing.*
> 

Imagine if **everyone** could issue their own IOUs in sats. 

You would accept promises only from well-known and verified peers—and only up to a certain amount. You would compare the risk of losing this money with the cost of bitcoin settlement.

This is basically a `cashu mint` living inside the app - without dedicated server and in basic setup without necessity of lightning node. Each instance would be able to issue users promises and  peers don’t need to be online at the same time.

 *Potentially it could be interoperable with cashu protocol - but research is needed.*

### 🦤 Nostr

Verified contacts need to communicate remotely. For that we could you nostr protocol. For contacts we are already using nostr `npub` as our identity. User sign his cashu tokens with private `npriv` related to same `npub`. And users are exchanging these tokens via nostr relays - probably using private messages (specified in [NIP-59](https://github.com/nostr-protocol/nips/blob/master/59.md))

Combination of 🫂Verified Contacts, 🥜Cashu Mint, and 🦤 Nostr enables that anyone can issue empty promises to his verified peers who accept it as a regular payment if they trust sender with the later settlement.

## 🤝 Settlement

### 🫥 Without settlement

Sometimes its not needed to settle the promises. Amounts might be too small or more promises might clear out.

1. Alice sends  1.000 sat to Bob. 
*I will type it as 1 kA which means 1 thousand satoshis promised by Alice.*
    1. On-chain transaction would cost Alice circa 500 sat which is 50%
    2. *Bob could request for this settlement too, but prefers the risk over costs*
2. Later on Bob pays to Alice 1.200 sat
    1. Bob uses his previously earned 1 kA and issue 0.2 kB on top off that.
    2. Promise differences are now bellow the dust. It’s not economical to settle this difference under the current circumstances.

| ![](https://github.com/hynek-jina/Hynek/blob/main/images/cashu_factory%200.png) | ![](https://github.com/hynek-jina/Hynek/blob/main/images/cashu_factory%201.png) |
|---|---|
| <sub> Bob has 1.000 sat promised from Alice </sub> | <sub> Bob paid to Alice with her previous promise and added 200 sat of his promises on top of that </sub> |

### 👴 On-chain

You might have notice in previous example that settlement could be triggered by any peer. Generally costs of bitcoin transactions are paid by sender. Here can peers negotiate any split ratio.

1. Alice pays 100kA to Bob
2. Bob is worried about whether he'll actually get it, so he decides to pay the transaction fee.
3. Alice then sends Bob 99.500 sat on-chain in exchange for previously issued 100kA promises

Bob paid 500 sat for the settlement, but it could be Alice, or they could split the cost in any ratio. During times of cheap block space, like now, you could settle on-chain more frequently and lower the risk of having promise instead of solid bitcoin. With increased cost you can prefer to risk more instead of high payment.

### ⚡ Lightning

Up until now we were discussing p2p transactions only. We want to achieve connection with the whole lightning network which is currently leading convention for bitcoin payments. 

*We already assume having server-less mint - build in every app instance. Lightning would be probably even more challenging. There are existing solutions like Zeus with integrated Lightning Node inside mobile app. Or we could utilize LSP (Lightning Service Provider) like ACINQ or Breeze. However we need the option to open channel to other peers, not only to selected LSP.* 

→ research and development is needed, but for now let’s assume that it is feasible 🤞

We want to simplify option to open LN channel directly to specific verified peer based on existing transaction history. Once you have at least one open channel you are motivated to burn as many promises as possible in this channel. It’s means no additional cost and it lowers the risk.

You don’t have to open channel to perfectly connected and the biggest channel, but rather one that you are interacting with most. This could extend the reach of the Lightning Network, connect the missing points, and, over time, help build a truly resilient network. 

<table>
  <tr>
    <td>
      <b>Channel Opening</b>
      <br><br>
      <ul>
        <li>Alice pays 100kA to Bob</li>
        <li>Alice pays 20kA to Carlos</li>
        <li>Carlos pays 20kC to Bob</li>
        <li>Bob has quite a lot of promises. A significant portion of them are from Alice.</li>
        <li>Bob swaps 20kC for 20kA</li>
        <li>Bob asks Alice to open a channel of 120k.</li>
      </ul>
    </td>
    <td>
      <img src="https://github.com/hynek-jina/Hynek/blob/main/images/cashu_factory%202.png" width="260">
      <img src="https://github.com/hynek-jina/Hynek/blob/main/images/cashu_factory%203.png" width="260">
      <br>
      <sub>Opened channel between A&B with all liquidity on B side and no promises in the economy</sub>
    </td>
  </tr>
</table>



**Cashu clearing**

- Bob pays another 20kB to Carlos
- Carlos pays 20kC to Alice
- Alice now has 20kC - she can claim them on-chain. However it costs 500 sats.
- Alice also has the more efficient option of exchanging 20kC for 20kB. And claim these Bob tokens immediately via LN.

| ![](https://github.com/hynek-jina/Hynek/blob/main/images/cashu_factory%204.png) | ![](https://github.com/hynek-jina/Hynek/blob/main/images/cashu_factory%205.png)|
| --- | --- |

**Cashu could be used as an extension for LN**

- There are channels between A&B, and also between C&D
- B and C are verified contacts, but not having opened LN channel
- A can pay to D even though there is no LN path between them
- In this case C would accept promise from B

![Initial state before the transaction](Channel%20Factories%20fueled%20by%20Cashu%20177dc526060680128c60de8c381e150b/image%206.png)

Initial state before the transaction

![Alice sent 10.000 sats to David. Carlos received promise from Bob and paid “for him” to David. Carlos would probably demand here higher fee in this scenario. Or lower if that transaction wouldn’t  increase the needed trust but decrease it.](Channel%20Factories%20fueled%20by%20Cashu%20177dc526060680128c60de8c381e150b/image%207.png)

Alice sent 10.000 sats to David. Carlos received promise from Bob and paid “for him” to David. Carlos would probably demand here higher fee in this scenario. Or lower if that transaction wouldn’t  increase the needed trust but decrease it.

We can potentially use alternative  settlements in the future - like Ark or side chains, or who knows what. But our aim here is to separate the logic of the individual transaction and the subsequent settlement. This allows us to make settlement smarter and thus cheaper.

### 🏭 Channel Factories

If we want to onboard all the people into bitcoin, lightning is not enough. However Channel Factories are here to fill this last missing piece. CF means that more people share the one multisig UTXO and from that they have virtual channels. Liquidity can be changed not only between each channels, but also between whole factory. This enable almost endless scaling.

Factories can be built between verified contacts—either at a scale where everyone trusts everyone or where each participant has at least two trusted contacts in the network. Some degree of trust is valuable for bridging uncertainty when peers optimize virtual channels. The ability to communicate and recognize each other further enhances security.

**Open Chanel Factory**

- A, B, C, and D has opened `CF`
- Each peer has two balanced virtual channels.

![image.png](Channel%20Factories%20fueled%20by%20Cashu%20177dc526060680128c60de8c381e150b/image%208.png)

When someone needs to rebalance his channel. They can freeze current state - temporary swap for from LN channels to issuing cashu tokens. And once all participants agree on a new set of virtual channels everything can be again settled on LN.

This way most onboarded people will not need to make an on-chain transaction which reveals a place for later users and more niche optimizations. ☀️
🦤 Nostr simplifies p2p communication between 🫂Verified Contacts. They issue and exchange 🥜Cashu tokens to optimize settlement, gradually building a resilient network.
