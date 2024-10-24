# Patricia Merkle Tries

## Intro

Bitcoin was the first blockchain-based decentralized network ever. It popularized the use of Merkle trees for scalable transaction inclusion. Ethereum also uses Merkle trees but since Ethereum is a completely different design, it also uses one other important tree data structure for some of its data storage needs: **Patricia Merkle Tries**.

This is the last data structure heavy day. If you've made it this far, you are doing fantastic! Patricia Merkle Tries are the first introduction into Ethereum-specific fundamentals, let's dive in...

## REVIEW: Bitcoin: Block Architecture

![bitcoin block](image-13.png)

In the previous section, we covered how Merkle trees are used to efficiently record a large amount of transactions into blocks, without needing to actually include them all - the merkleRootHash is all that is needed to commit those transactions.

## First Look: Ethereum Block Architecture

Bitcoin's architecture is simple: it's a ledger that keeps track of transactions using a UTXO model. Since Ethereum keeps track of a larger amount of state data, the block architecture is completely different:

![eth-block](image-14.png)

Why are you showing me block architectures, aren't we covering trees?

Well, because these blocks contain references to the tree data structures we are focusing on. The main goal here of showing the block architecture first is: by the end of this lesson, you should be familiar with three of the staple Ethereum block properties included in the diagram above: `State Root`, `Transaction Root`, Receipt Root - just like in the last section we covered what the `merkleRootHash` was in the context of a Bitcoin block, we will now look at three new similar tree uses in Ethereum.

- Woah, that's a lot of properties in an Ethereum block! Don't worry, we will cover these further in the bootcamp. We have to tackle the low-level ones first.

## REVIEW: Merkle Trees in Bitcoin

Merkle trees are fantastic for transactions. They are the perfect data structure. Transactions are static and should never change after being committed. They are "set in stone" via the Merkle hash root construction. Merkle trees are not a data structure fit for editing, so edit time -- how efficient it is to change a record -- does not matter here

The main goal behind their usage is to prove the consistency of data as the blockchain grows. Thanks to Merkle trees, we can rest assured that a transaction existed at one point in time in a block. How? Just by constructing the Merkle proof! Not only this, Merkle proof construction is extremely efficient at scale since they are computationally fast to compute and require only small chunks of data to be communicated over the network.

## Trees in Ethereum

Ethereum makes use a data structure called a [radix trie, also referred to as a Patricia trie or a radix tree](https://www.cs.usfca.edu/~galles/visualization/RadixTree.html) and combines this data structure with a Merkle tree to create a **Patricia Merkle Trie**.

- Patricia Trie + Merkle Tree = Patricia Merkle Trie (pronounced either "tree" or "try")

## Radix Trie

"Trie" comes from the word "retrieval", to give you a hint as to what Patricia Merkle Tries (also referred to as Patricia Merkle Trees) optimize for.

**A radix trie is a tree-like data structure that is used to retrieve a string value by traversing down a branch of nodes that store associated references (keys) that together lead to the end value that can be returned:**

![radix tree](image-15.png)

- In grouping associated keys together, our search for the end value is optimized and more efficient

## Patricia Merkle Trees

A **Merkle Patricia trie** is a data structure that stores key-value pairs, just like a [hash table](https://en.wikipedia.org/wiki/Hash_table). In addition to that, it also allows us to verify data integrity and the inclusion of a key-value pair.

- PMTs groups similar-value nodes together in the tree. That way, searching for "HELP" leads you along the same path as searching for "HELLO" - the first three letters are shared entries of different words. Good for space efficiency and read/write efficiency.

Patricia Merkle Trees are basically Merkle trees on steroids! Efficient for data verification needs, but also efficient for editing that data.

Patricia??

- P = Practical
- A = Algorithm
- T = To
- R = Retrieve
- I = Information
- C = Coded
- I = In
- A = Alphanumeric

![Patricia-Merkle](image-16.png)

The root node of this PMT is empty so we can store other words not starting with ‘n’, like "apple" or "hello".

## Why Does Ethereum Use a Merkle Patricia Trie?

There are typically two different types of data:

- **Permanent**
    - Once a transaction occurs, that record is sealed forever 
        - This means that once you locate a transaction in a block’s transaction trie, you can return to the same path over and over to retrieve the same result

- **Ephemeral**
    - In the case of Ethereum, account states change all the time! (ie. A user receives some ether, interacts with a contract, etc)
    - `nonce`, `balance`, `storageRoot`, `codeHash`

It makes sense that permanent data, like mined transactions, and ephemeral data, like Ethereum accounts (balance, nonce, etc), should be stored *separately*. Merkle trees, again, are perfect for permanent data. PMTs are perfect for ephemeral data, which Ethereum is in plenty supply of.

Unlike transaction history, Ethereum account state needs to be frequently updated. The balance and nonce of accounts is often changed, and what’s more, new accounts are frequently inserted, and keys in storage are frequently inserted and deleted.

## Ethereum Block Header

The block header contains many pieces of data. Remember back to Week 1 PoW Mining? The block header is the hash result of all of the data elements contained in a block. It's kind of like the gift-wrap of all the block data.

If you look at the Ethereum architecture diagram at the beginning of this lesson, the block header ends up hashing all of the data properties of the block. It also includes:

- **State Root**: the root hash of the state trie
- **Transactions Root**: the root hash of the block's transactions
- **Receipts Root**: the root hash of the receipts trie

## Ethereum: State Trie

![state trie](image-17.png)

As shown in the above diagram, **the state trie acts as a mapping between addresses and account states**.

It can be seen as a global state that is constantly updated by transaction executions. All the information about accounts are stored in the world state trie and you can retrieve information by querying it.

Account Example:

As mentioned above, the state trie is just a mapping that uses an address as the key and the account state (nonce, balance, etc) as the value returned.

![account example](image-18.png)

This is what you would get back from a JavaScript request to the Ethereum world state. Just an object containing some data! That is all the account state is... but this is too much data to store in each block, so a root hash of it commits the data per block.

## Ethereum: Transaction Trie

**The transaction trie records transactions in Ethereum**. Once the block is mined, the transaction trie is never updated.

![Transaction Trie](image-19.png)

Each transaction in Ethereum records multiple pieces specific to each transaction such as `gasPrice` and `value`.

Transaction Example:

You've probably seen this via services like Etherscan! All these services do is query the Ethereum blockchain for transaction data and then index it into an organized transaction viewer.

![transaction trie](image-20.png)

You can even try querying the transactions trie directly using [Alchemy Composer](https://composer.alchemy.com/). Just take a random tx hash and use the `eth_getTransactionByHash` method - you'll get a response looking much like the object in the picture above.

## Ethereum: Transaction Receipt Trie

**The transaction receipt trie records receipts (outcomes) of transactions**. Data including `gasUsed` and `logs` (events emitted are contained here!).

Once the block is mined, the transaction receipt trie is never updated.

Transaction Receipt Example:

![transaction receipt](image-21.png)

Try it out on the [Alchemy Composer](https://composer.alchemy.com/) - just make sure to change the method to `eth_getTransactionReceipt`.

## Conclusion

![block and trie graph](image-22.png)

The above diagram is an excellent visualization into how the tries all end up being committed in every block via their root hash. The raw data is stored elsewhere in Ethereum, particularly [archive nodes](https://www.alchemy.com/overviews/archive-nodes).

Take a look back over the various architectures included in this lesson! Does the Ethereum block architecture diagram look less threatening? If so, good! We are learning as we go and we've just covered some of the lowest-level aspects of Ethereum data storage. Very few people learn these fundamentals. These are super important! Not only does learning them give you a more holistic understanding of Ethereum, this is knowledge applicable in all of computer science and even physics.

The important takeaway of this lesson is to understand why the low-level data structures used by Ethereum are used: to optimize data space and read/write efficiency.


## Merkel Trees in Ethereum Review

Here is a [technical overview](https://blog.ethereum.org/2015/11/15/merkling-in-ethereum/) of merkling in Ethereum by Vitalik Buterin. Vitalik highlights several reasons for using Patricia Merkle Tries in Ethereum:

- Efficient data verification (from its merkle properties)

- More complex light-client queries

- Can quickly change values and only recompute a portion of the tree (prevents some DDOS attack vectors)

- There is a limit to the depth of the tree, which prevents other DDOS attack vectors

- The order of the updates do not matter for the root hash

Ethereum nodes maintain four tries:

- A **state trie** which contains information about Ethereum accounts

- A **storage trie** which is where we can write persistent data from smart contracts

- A **transactions trie** which contains the transactions stored in a block

- A **receipts trie** which contains log/event information from contracts

Here is a [good overview of Patricia Merkle Trees on Medium](https://medium.com/shyft-network-media/understanding-trie-databases-in-ethereum-9f03d2c3325d). This article references some images from a stack overflow answer which are extremely helpful to look at!

- This starts with a good overview and quickly gets highly technical! Read as far as you are interested, we will not need to know the exact details of the Ethereum data storage implementation.

## Quick Note on RLP

We're going to be seeing RLP come up quite a bit. This is a serialization format used in Ethereum, you can think of it like JSON. It is used to send data from one machine to another in a format where the machine knows how to parse the data.

You can find more information on [RLP here](https://ethereum.org/en/developers/docs/data-structures-and-encoding/rlp/).

- As the docs here point out "In summary, RLP is like a binary encoding of JSON, if JSON were restricted only to strings and arrays."