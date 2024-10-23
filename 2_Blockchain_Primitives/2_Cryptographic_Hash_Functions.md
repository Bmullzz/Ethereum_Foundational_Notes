## What is the purpose of blockchain?
- The purpose of a blockchain is to have a **network of computers agree upon a common state of data**. Plain and simple. Any person or organization should be able to participate in this process. No person or organization should be able to control this process.
    - Generally the term consensus is used to describe a network coming to an agreement on the state of the data. You'll hear this word quite often in regards to blockchain.

## Why is blockchain needed for cryptocurrency?
- To understand why blockchain is needed for digital currencies let's imagine a naive digital currency without blockchain. 

Let's take a spreadsheet and give all our friends some money:

| **Name** | **Balance** |
|----------|----------   |
| Alice    |  10         |
| Bob      |  10         |
| Charlie  |  10         |

- Everyone starts with 10 money.
- Now Alice wants to buy something from Bob, so she pays him 5 money. She tells you (the bookkeeper) to transfer 5 monies over to Bob.

Now you adjust the ledger to reflect this change: 

| **Name** | **Balance** |
|----------|----------   |
| Alice    |  5          |
| Bob      |  15         |
| Charlie  |  10         |

Everyone's balances are updated.

- At this point you might be thinking "There really isn't much to this whole digital currency thing!". Or, more likely, you're considering all the problems with this scenario:
    1. Alice, Bob, and Charlie need to **trust** that you won't cheat them. As the bookkeeper you need to be resistant to bribes!
    2. Alice, Bob, and Charlie need a way to easily view their balance that is widely available and up-to-date.
    3. Alice, Bob, and Charlie invite more friends into your currency circle and quickly the bookkeeping becomes too much for you to handle.

- We know how to solve **problems #2 and #3** with our programming skills! We can build a website with an awesome UI and an API for making transactions! 

- But what about **problem #1**? How do we solve for **trust**?

- This was a problem that ate at Cryptography Enthusiasts for years. Deep down, many self-proclaimed [Cypherpunks](https://en.wikipedia.org/wiki/Cypherpunk) felt as though the solution was somewhere in the land of cryptographic technology, yet nobody was able to create a foolproof system.

- In, 2008, such a system was imagined. A person or persons, under the pseudonym **Satoshi Nakamoto** released a whitepaper [whitepaper for Bitcoin](https://bitcoin.org/bitcoin.pdf). In this paper they described a system that would create a peer-to-peer network for exchanging value. This system would combine years of cryptographic research and game theoretical financial incentives to create a secure, scalable network. The paper describes a chain of blocks tied together cryptographically. This would later be coined the **blockchain**.

- To tie it altogether, blockchain was invented to solve for trust. To create a system that is completely neutral and resistant to any censorship or bribe.

## Smart Contract Blockchains
- Smart Contract blockchains provide developers with a way to decentralize where the code runs. In this way, code can truly become a public resource. This means code can run without any direct ownership, making it censorship resistant and transparently verifiable.
- One important point to drill home is that the decentralization isn't about the code itself, but how the code is executed. For example, let's take a quick glance at some Solidity smart contract code:

```solidity
// this data structure will keep track of which address has a balance
mapping(address => uint) balances;

function transfer(address to, uint amount) external {
  // subtract the amount from the sender's balance
  balances[msg.sender] -= amount;

  // add the amount to the recipient's balance
  balances[to] += amount;
}
```