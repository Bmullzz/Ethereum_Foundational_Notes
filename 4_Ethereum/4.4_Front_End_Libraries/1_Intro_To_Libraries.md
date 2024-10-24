# Introduction to Ethereum Front-end Libraries

Virtually every web3 website, or dapp that you have ever used uses one of [web3.js](https://web3js.readthedocs.io/en/v1.8.1/) or [ethers.js](https://docs.ethers.io/v5/). Together, they are the two most popular Ethereum Javascript libraries that allow developers to interact with Ethereum or EVM-compatible blockchains using the JSON-RPC (Javascript Object Notation- Remote Procedure Call) protocol.

In other words, these are JavaScript libraries that allow you to do things that fundamental to almost every dapp: deploy smart contracts, create wallets, sign transactions, query the blockchain, etc. without having to make raw API calls to the blockchain.

One of the most common questions developers ask when starting out with web3 development is which library to use in their projects. In this guide, we will cover what ethers.js and web3.js libraries are, what they can do, and how they differ so you're able to make a choice depending on the requirements of your project.

- If you're using Ethers.js but you also want access to certain Alchemy-specific features such as our [NFT API](https://docs.alchemy.com/reference/nft-api-faq), [Enhanced WebSockets](https://docs.alchemy.com/reference/sdk-websockets-endpoints), [Transact features](https://docs.alchemy.com/docs/alchemy-transact), or [Token API](https://docs.alchemy.com/reference/token-api-quickstart), read on!

- We built a strict superset of Ethers.js that makes it simple to integrate your Ethers.js code into Alchemy's custom endpoints, called the Alchemy SDK. You'll get the same syntax and features as Ethers while gaining access to Alchemy's best-in-class infrastructure and Enhanced APIs.

- [Alchemy SDK Quickstart](https://docs.alchemy.com/reference/alchemy-sdk-quickstart)

## Advantages of ethers.js