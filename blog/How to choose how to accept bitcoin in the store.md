# How to choose how to accept bitcoin in the store?

Whenever I pay somewhere, I try to use bitcoin. I usually fail, but sometimes we at least get into a discussion about how to actually do it. In that case, it seems like there are a lot of options and I usually can't give a simple answer.

My basic decision scheme looks something like this:
![Jak přijímat bitcoin-2](https://github.com/hynek-jina/Hynek/assets/26002916/ad4fc052-1173-47ca-aa71-8fee509a758a)


I start at the top left by asking if the business has multiple people accepting payments. Depending on the answers, I continue to wander through the diagram until I arrive at a final recommendation.

Of course, it's not black and white like this. Sometimes the conversation is more complex. Basically, I then distinguish between these four groups of tools:

## Custodial wallets
In most cases, we choose a simple wallet first, on which one can easily and without cost try it out. After a while, it is no problem to move to a more sophisticated solution. For several years now, Wallet of Satoshi has been my favorite to start with.

### [Wallet of Satoshi](https://www.walletofsatoshi.com/)
- 🟢 Great controls
- 🟢 POS terminal
- 🟢 Low fees
- 🟢 Local language
- 🟢 Expression in local currency
- 🟢 Option to receive funds to a simple address
- 🟢 Possibility of accepting NFC chips - cards, rings, etc.
- 🟢 Multiple people can use one account - You can have the same wallet on your computer (mac)
- 🟢 Easy email backup
- 🔴 You trust a third party - you can lose funds

[Bitlifi](https://www.bitlifi.com/) works similar. Its big advantage and disadvantage is that it is tied to a phone number. This allows you to pay people who haven't even downloaded the app yet. On the other hand, you lose privacy. Bitlifi can practically only be used by one person because of this, and it also doesn't have advanced options like using NFC chips.

## Wallets with self-custody
If you don't want anyone to be able to deprive you of your funds, you can use a wallet such as the Phoenix wallet.

### [Phoenix](https://phoenix.acinq.co/)
- 🟢 You are in control of your money, no one can easily rob you
- 🟢 Easy to use
- 🟠 Each recipient has an independent account
- 🔴 High fees
- An alternative may be the [Breez](https://breez.technology/) wallet. It has slightly lower fees while offering more privacy. It also allows you to create items for easier payment entry in addition to a traditional POS terminal. On the other hand, it can be less clear and downloads more data. Both of the mentioned wallets work practically for one user only and are more expensive to use than the previous options.

## Friends server
Financially, using a friends node or LNbits server usually works out a bit better. This solution offers virtually unlimited possibilities.

### [LNbits](http://lnbits.com/)
- 🟢 Many users and their management
- 🟢 Many different applications
- 🟢 API for communication with other applications
- 🟢 Can be connected to [Zeus](https://zeusln.app/) or [Blue Wallet](https://bluewallet.io/)
- 🟢 Allows to manage [Bleskomat](https://www.bleskomat.com/)
- 🟢 Can create QR codes for individual items
- 🟡 Usually reasonable fees
- 🟠 Unclear reliability
- 🟠 It's a bit too much work to set it up
- 🔴 Trusting a third party - you may lose resources (if running on someone else's server)

If you don't want to play with LNbits, you can use a dedicated service like [Hydranode](https://hydranode.net/), [Confirmo](https://confirmo.net/), or [Qerko](http://qerko.com/) to receive bitcoin. They will help you with deployment, you'll have a good overview of everything and various staff permissions for reasonable fees.

## Own node

### Umbrel
For the heartthrobs, there is the most challenging option. On your own node, you can then also run the aforementioned LNbits application.

- 🟢 You don't trust a third party
- 🟢 Everything is possible
- 🟢 Lowest fees
- 🟢 Good overview of everything - different powers for staff
- 🔴🔴 High initial cost - hardware and especially your education
- 🔴 Time-consuming maintenance


Here's another summary of the mentioned options side by side. I don't know the universally best solution, but each of the variants has good uses.

|   | Custodial wallets | Non-custodial Wallets | Friends Node | Own Node |
| - | ----------------- | -------------------- | ------------ | -------- |
| Examples | Wallet of Satoshi, Bitlifi | Phoenix | LNbits | Umbrel |
| Difficulty of setup | 🟢 | 🟢 | 🟠 | 🔴🔴 |
| User Management | 🔴 | 🔴 | 🟢 | 🟢 |
| Custody | 🔴 | 🟢 | 🔴 | 🟢 |
| Fees | 🟢 | 🔴 | 🟠 | 🟡 | 🟡 |


### When the internet is down
As a backup, it's always a good idea to have a physical QR code printed at the same time with the so-called LNURL or at least remember the payment address. For these purposes, it's also not a problem to use a wallet with a third-party escrow service like Wallet of Satoshi - still only for small amounts of satoshis. If for some reason your internet goes down or your cell phone goes dead, you can still accept bitcoin payments with no problem.

### Alternatives
There are many other technical options that make sense to pursue. But since I don't use them on a daily basis, I don't usually recommend them. For example, I think [Coinos](https://coinos.io/), [Mutiny](https://www.mutinywallet.com/), [Blixt](https://blixtwallet.github.io/), [Zeus](https://zeusln.app/), [BTCPay Server](https://btcpayserver.org/), or [Citadel node](https://runcitadel.space/) are all worth considering.

### Don't take fiat or you'll go crazy
I generally try to talk dealers out of converting bitcoin to fiat. Usually, at least initially, bitcoin payment volumes are not large and the real-world consequences of volatility are negligible. If someone doesn't want to hold bitcoin, they can get a Bleskomat into the business and allow people to exchange. After a while, though, merchants are usually glad they kept the funds in bitcoin and don't have as much need to convert back to fiat.

If you're worried about the complexity of accounting when a company holds bitcoin, you can use one of the services mentioned above or not put bitcoin in the company at all and handle it as a private person.

_I originally wrote this article for a [Jednadvacet](https://jednadvacet.org/blog/), Czech bitcoin community_
