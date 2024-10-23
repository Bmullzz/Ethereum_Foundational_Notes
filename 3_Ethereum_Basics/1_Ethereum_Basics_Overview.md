## Overview
- Accounts in Ethereum
- Ethereum Transactions
- Gas and fees in the Ethereum network
- Overview of Ethereum Structure


### Lesson 3.1 - Accounts
-In Ethereum, the state is made up of objects called accounts, with each account having a 20-byte address.

- State Objects
	- Externally owned accounts
		- State: Balance
		- Address: 12 hexidecimal
		- Balance: 10 ETH
		- TransactionCount(Nonce): 3

	- Contract Accounts
		- State: Balance & Storage
		- Address: 
		- Balance: 50 ETH
		- Account Creation Count (Nonce): 30
		- Storage: (...)
		- Contract Code:

- External Accounts
	- Owned by people
- Contract Accounts
	- Deployed contracts

- Externally Owned Accounts
	- 1. Ether Balance
	- 2. Send Transactions
		- >Transfer Value
		- >Initiate Contract Code
	- 3. Controlled by Private Keys
	- 4. Nonce

- Contract Accounts
	- 1. Ether Balance
	- 2. Can transfer value
	- 3. Can call other contracts
	- 4. Associated Smart Contract
		- Initiated by external transactions
		- Can manipulate Storage
	- 5. Nonce

- Externally Owned Accounts:
	- Whenever a user generates a private-public keypair, a corresponding account address is created as well.
- An External Account is used to deploy contract accounts

- Contract ```CREATE``` opcode
- ```CREATE2``` 
	- Uses different info to determine a contracts address
	- Allows for offchain scaling solutions



### Lesson 3.2 - Transactions
- A message sent from one account to another
	- Transactions update state
		- Ether balance
		- Contract Storage
	- Always signed by sender
	- EOA or Contract Account
	- Optionally includes
		- Ether 
		- Data
- If the target is a contract
	- Code executes with data as input

- If target account is 0 or 0x0 
	- Transaction creates new contract
	- Transaction data is executed
		- Output is stored as the contract
- Ethereum Transaction Contents
	- Recipient Address
	- Nonce (transaction count from sender)
	- Cryptographic Variables: V, R, S
	- Make up the sender's signature 
	- Value (Optional):  100000 (in wei)
		- Amount of Ether to send with a transaction
	- Data (Optional):
		- Specifies contract instructions or deployment instructions
	- Gas Limit or Start Gas
		- The maximum number of computational steps the transaction execution is allowed to take
	- Gas Price
		- the fee the sender pays per computational step


### Lesson 3.3 - Gas and Fees
- Executing operations on Ethereum costs a fee 
	- The network is like a public utility, like the electric grid
	- Gas fees are incentives for miners
	- Miners collect all gas used in a block as a reward
- Gas is the metering unit of the Ethereum Virtual Machine
- Each operation on the EVM consumes gas 
	- Different operations cost different amounts
	- Multiplication consumes 5 gas
	- Addition consumes 3 gas
- Gas is paid with Ether
- Gas limit and price is specified per transaction
- Gas limit is max gas allowed for the transaction
- Gas price is how much ether the sender pays per gas

- Gas usage
	- Every operation consumes a predetermined amount of gas
	- Set transaction gas limit at the beginning of a transaction
		- Start gas/gas limit
		- Start gas is sent with the transaction to pay for processing
	- Every operation consumes gas
		- Remaining gas is reduced every step

- Out of gas 
	- Transactions that run out of gas with steps remaining will fail

- Successful transaction
	- Remaining gas is returned to the sender of the transaction

- Fees help protect the network
	- Reduce spam
	- Halt the code
	- Every step costs something
	- Infinite loops will run out of funds
- Eth gas station



### Lesson 3.4 - Ethereum Structure
- Open source, public network
	- Anyone can download the software to set up a node
	- Permissionless
		- Anyone can join or contribute
	- Blockchain features provide:
		- State management 
		- Trustlessness
		- Trackability
		- Irreversable
	- The Ethereum Virtual Machine
		- Execution environment
	- Ideal system for smart contracts

- Distributed Computing
	- Ethereum Virtual Machine (EVM)
		- Runs on every node
		- Handles all transaction processing
		- Turing Complete
		- Operates on bytecode
	- The EVM is slow
		- 10-20 transactions per second
		- Every Transaction is processed by every node
		- Slow and fast computers
		- Only as fast as the slowest machine

- EVM bytecode
	- The EVM executes bytecode
		- Bytecode is a low level stack based language 
			- Bytecode specifies how state transitions are applied to the network's state
		- Transactions contain bytecode
	- ADD SCREEN SHOT

- Smart contracts exist as bytecode
	- Contract accounts keep contract bytecode in storage
	- EVM executes contract bytecode when a transaction is received

- Transaction Data -> Contract Account -> EVM -> Updated system

- High level languages compile to bytecode
	- Solidity
	- Vyper
	- LLL

- Ethereum Network Process
	- Transactions are broadcast to the network
	- Grouped into sets called blocks
	- When a valid block is found, the block is broadcast with:
		- Transaction list
		- Uncles list
		- Block Header:
			- Previous block hash
			- State root
			- Transactions root
			- Receipts root
			- Block number
			- Gas used
			- Timestamp
			- Nonce

- Block Uncles
	- Uncles are a consequence if Ethereum's short block time and proof of work
	- A discovered block not included in the main chain is an Uncle
	- A block is found every ~15 seconds
		- Low difficulty causes simultaneous discovery 
		- Network delays cause a disadvantage
			- Nodes that get the message of the discovered block get a head start on mining a new block
	- Discovering uncle blocks is rewarded
	- Incentive to stay decentralized 
		- Makes mining pools unattractive

- Ethereum as a platform
	- Turing Completeness allows for smart contracts
	- Digital Identity Management
	- Value Transfer
	- Applications on Ethereum 
		- Use the underlying Ethereum security
		- Benefit from Ethereum protocol development
	- Interoperability

- Ethereum Road Map
	- Frontier (2015)
		- Bare bones, not usable for non-technical people
	- Homestead
	- Currently in Metropolis stage 1
		- Bysantium
			- Enhanced privacy features
		- Stage 2: Constantinople
			- Expected in 2018
	- Final Phase: Serenity
		- Proof of Work -> Proof of Stake
			- Casper
			- Scaling solutions


### Lesson - 3.5 - Externally Owned Accounts and Ethereum Transactions
- Interactive notebook
- In this lesson, we are going to introduce how to programmatically use the front end library, web3.js, to create Ethereum accounts and sign transactions,
- This javascript library can be used for many Ethereum related actions including handling accounts and sending transactions
- Metamask is required


### Lesson 3.6 - Generating Ethereum Addresses
- Generating Ethereum Accounts in Javascript
- 