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

-  This function is the bread and butter of ERC20 tokens, which we'll talk about later in the course. You'll see there's nothing special about the `transfer` function here from a programming standpoint. Coming from other languages this code may look quite familiar.
- The key difference which makes this code a **smart contract** is when you take this code, compile it and deploy it to a decentralized blockchain. When you do that, the code becomes publicly available on the blockchain and the nodes in the network will enforce the logic of the code through the financial incentives of the blockchain protocol.
- A key takeaway here is that a smart contract is code that will always run the way it is programmed. We'll take this one step at a time and you'll soon see how blockchains enforce those rules.

## Cryptographic Hash Functions
- Before diving any further we must understand the cryptographic hash function. Let's break this term down a bit. A hash function is a function which takes an input of any size and turns it into a fixed size output. Let's imagine a hash function that takes an input of any size and returns a fixed 32 byte output:

| **Input**       | **Input Size**  | **Output** | **Output Size** |
|----------       |----------       | ---------- |  ----------     |
| 52              |  8 Bytes        |  0x41cf... |  32 bytes       |
| "happy times"   |  22 Bytes       |  0xd6bf... |  32 bytes       |
| monalisa.jpg    |  875000 Bytes   |  0x7cde... |  32 bytes       |
| worldseries.mp4 |  1.6e+10  Bytes |  0x9c0e... |  32 bytes       |

- These inputs get larger from top to bottom but they always map to an output of 32 bytes. There are many different [algorithms for hash functions](https://en.wikipedia.org/wiki/Hash_function#Hashing_integer_data_types) which could take these inputs and create outputs of fixed sizes.

- The specific types of hash functions we are going to focus on are cryptographic hash functions. These hash functions need five specific properties. They must be:
    - **Deterministic** - One specific input always maps to the **same** specific output
    - **Pseudorandom** - It is not possible to guess the output based on the output of similar inputs
    - **One-way** - If someone gives you a new output, you could not determine an input without guessing
    - **Fast to Compute** - It must be a quick calculation for a computer
    - **Collision-resistant** - The chance of a collision should be infinitesimally small

    - Try this [sha256 online](https://emn178.github.io/online-tools/sha256) tool to prove each one of these properties to yourself. 

    - With a secure cryptographic hash function you can create a unique, fixed-size representation of an input regardless of its size. For blockchains this feature is critically important for saving space. In many cases blockchains and smart contracts will not need to store an input, they can just store the hash output. Cryptographic Hash Functions will also be super important for the first successful blockchain consensus mechanism we'll talk about: **proof of work**.