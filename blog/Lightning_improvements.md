## List of Lightning Network improvements

What is happening? I don't actually know. So this is an effort to navigate the Lightning Network [LN] ⚡.

#### How currently LN works?
- I want to open a channel to someone
- Together we create a 2/2 multisig address
- We'll set up a closing transaction from which all the funds go to me
- I then send bitcoin to this multisig address in the agreed amount

![image](https://github.com/hynek-jina/Hynek/assets/26002916/53184aa8-f561-448b-b9f3-5fab705c6c4e)

**What is the problem?**
It works nice.. But it can be costly, transactions are failing sometimes, you need to lock a lot of liquidity, be always online and so on...

### Proposals
How to make it more effective (cheaper)

#### 1. Growing and shrinking channels
![image](https://github.com/hynek-jina/Hynek/assets/26002916/0e214516-b34a-4175-aa05-fce4ce6f1c0d)

#### 2. Opening of more channels with one transaction
![image](https://github.com/hynek-jina/Hynek/assets/26002916/1d6987c1-a3f6-4818-ac79-d684a40e7898)

#### 3. Closing of more channels with one transaction
#### 4. Opening and closing with one transaction
#### 5. Adding output into closing transaction
#### 6. More owners of one channel
#### 7. More owners of one UTXO - (ie [Ark](https://www.arkpill.me/))
