# Supplemental Reading

We covered a whole lot in this section! Here are a few additional resources for you to go more in-depth on topics we discussed or learn about totally new areas we didn’t cover.

## Node Clients

Node client software is a crucial aspect to accessing the blockchain. Having a diverse set of node clients helps reduce risk factors of just using one. For example, if 100% of all nodes were running Geth and Geth had a vulnerability or bug it would put the entire chain at a risk. However, if the other node clients like Eigon or Nethermind are still working as expected, we can rely on those clients to maintain the integrity of the network.

If you’re interested in seeing a breakdown of how many nodes are running each client in the network check out https://ethernodes.org/

Since we’re using Alchemy for our development we don’t need to worry about which node client to choose or maintaining multiple different clients to reduce risk.

Luckily, Alchemy runs a variety of node clients under the hood so if one were to have an issue we can always fall back on other ones. This also allows us to be able to use one API key for different API endpoints that are only available on unique clients. For example, with our single Alchemy API key, we can make requests to both the Trace API (unique to Erigon) and the Debug API (unique to Geth) without having to run or enable those respective node clients individually.

## The History of Ethereum

Here is an overview of key events that occurred on the Ethereum chain since inception. If you’re interested in learning more about the History of Ethereum check out the Infinite Machine by Camilla Russo.

![History](<Screenshot 2024-10-24 at 12.09.55 AM.png>)

## Ether: Ultrasound Money

As we learned in the Gas on Ethereum section, Ether is now burned after transactions are included in blocks. This has a unique property of making Ether a deflationary asset since supply is being removed from circulation.

If you’re interested in learning more about Ether as “Ultrasound Money” check out https://ultrasound.money/ which gives you a breakdown of the amount of ether burned and amount of supply in circulation.

## Use cases of Ethereum

If you’re taking this course you’re probably well aware of all the potential use cases of Ethereum. Here are a few that are helpful for understanding, however, this list is pretty much infinite.

1. Ownership records

    1. permanent way to verify ownership of a house or other asset

2. Code

    1. ability to deploy code to a public database where all parties can verify the functionality of it before buying in

3. Other popular areas: 

    1. Decentralized finance
    2. NFTs
    3. DAOs
    4. Further applications

## Other Resources

There are tons of awesome resources about Ethereum and the EVM on the internet. Here are a few places we recommend you check out to learn more:

- [Ethereum Whitepaper](https://ethereum.org/whitepaper/)
- [Ethereum Yellowpaper](https://ethereum.github.io/yellowpaper/paper.pdf)
- [Ethereum Beigepaper](https://github.com/chronaeon/beigepaper)
- [ethereum.org](https://ethereum.org/en/)
- [Alchemy Overviews](https://www.alchemy.com/overviews)
- [Alchemy Dapp Store](https://www.alchemy.com/dapps)
- [Alchemy Developer Hub](https://docs.alchemy.com/)
- [EVM opcodes](https://github.com/crytic/evm-opcodes)
- [A pre-history of Ethereum](https://vitalik.ca/general/2017/09/14/prehistory.html), if you're interested in the initial design decisions
- [Patricia Trie Specification](https://ethereum.org/en/developers/docs/data-structures-and-encoding/patricia-merkle-trie/)
- [Design rationale of Ethereum](https://ethereumbuilders.gitbooks.io/guide/content/en/design_rationale.html)
- Andreas Antonopoulos' [Ethereum Book](https://github.com/ethereumbook/ethereumbook)
