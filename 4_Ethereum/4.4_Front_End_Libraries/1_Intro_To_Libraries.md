# Introduction to Ethereum Front-end Libraries

Virtually every web3 website, or dapp that you have ever used uses one of [web3.js](https://web3js.readthedocs.io/en/v1.8.1/) or [ethers.js](https://docs.ethers.io/v5/). Together, they are the two most popular Ethereum Javascript libraries that allow developers to interact with Ethereum or EVM-compatible blockchains using the JSON-RPC (Javascript Object Notation- Remote Procedure Call) protocol.

In other words, these are JavaScript libraries that allow you to do things that fundamental to almost every dapp: deploy smart contracts, create wallets, sign transactions, query the blockchain, etc. without having to make raw API calls to the blockchain.

One of the most common questions developers ask when starting out with web3 development is which library to use in their projects. In this guide, we will cover what ethers.js and web3.js libraries are, what they can do, and how they differ so you're able to make a choice depending on the requirements of your project.

- If you're using Ethers.js but you also want access to certain Alchemy-specific features such as our [NFT API](https://docs.alchemy.com/reference/nft-api-faq), [Enhanced WebSockets](https://docs.alchemy.com/reference/sdk-websockets-endpoints), [Transact features](https://docs.alchemy.com/docs/alchemy-transact), or [Token API](https://docs.alchemy.com/reference/token-api-quickstart), read on!

- We built a strict superset of Ethers.js that makes it simple to integrate your Ethers.js code into Alchemy's custom endpoints, called the Alchemy SDK. You'll get the same syntax and features as Ethers while gaining access to Alchemy's best-in-class infrastructure and Enhanced APIs.

- [Alchemy SDK Quickstart](https://docs.alchemy.com/reference/alchemy-sdk-quickstart)

## Advantages of ethers.js

Ethers can do everything that web3.js can when it comes to interacting with the blockchain. In addition to that, it has a few more perks:

A Broader License
Ethers is available under the MIT License which not only allows developers to use it for free, but also allows modifications to it.

The latter is also allowed under the LGPL-3.0 license that web3 uses but it also forces you to release the source code containing the modifications.

Smaller Size

Ethers is an extremely lightweight library. It's only 77 KB compressed and 284 KB uncompressed.

ENS Compatible
Ethers knows how to parse ENS domain names by default. Therefore, you can replace a hexadecimal address with a .eth domain without any extra boilerplate code.

A Large Number of Test Cases
Ethers is extraordinarily well-tested, with close to 10,000 test cases; a significant chunk being written by Richard Moore himself. Ethers was a pioneer with respect to maintaining a well-tested Ethereum library (web3 has since managed to catch up to an extent).

## Drawbacks of ethers.js

Ethers is a relatively new library. Hence, it is hard to find it in use in older, more foundational projects and companies. If you work or are planning to work in such a company, it may be worthwhile to spend more time learning web3.

## When to Use ethers.js

Ethers is a fantastic library to use if you're building a new project. At the time of writing, the popularity (in terms of weekly downloads, beginner tutorials, and community support) has either surpassed or quickly catching up to that of web3.

Given the small size of the library, it is especially lucrative on the frontend as it can improve the performance of your website/app significantly.

## Important ethers.js Class Abstractions

These are the core class abstractions that you will need to use to write scripts that interact with the Ethereum computer. These are also the base abstractions that the Alchemy SDK uses 1-to-1.
