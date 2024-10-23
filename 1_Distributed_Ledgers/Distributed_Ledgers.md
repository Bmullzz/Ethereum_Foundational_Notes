# Overview
- Distributed ledgers and how they are different from traditional data storage options.
- Consensus mechanisms and how they secure distributed ledgers.
- How mining in the Proof of Work consensus mechanism secures a network.
- Difference between public and private blockchains.

## What is the purpose of blockchain?

## Module 1.1
- Distributed Ledgers
- Consensus Mechanisms
- Mining in Ethereum
- Public and private blockchains
- Blockchain platforms

### Lesson 1 - Distributed Ledgers
- Ledgers
	- Track accounting and value
	- Foundation of accounting
	- Stored in databases
		- Centralized
		- Data integrity
		- Speed
		- Accessability
- Database Transactions
	- Must be ATOMIC
		- This means that either ALL transactions are updated or NONE are.
		- All or nothing
	- Stored in DB, durable and consistent
- Distributed Ledgers
	- Data integrity
		- Public/Private key cryptography
- Transactions
	- Atomic
	- Durable
	- Consistent
	- Peers must agree on state
- A ledger is distributed when it has been securely replicated across geographic locations. Some features include: 
	- Consensus formation
	- Peer-to-peer protocols
	- Cryptographic infrastructure
- Blockchain Technology
	- A blockchain is one type of distributed ledger which uses blocks as the security mechanism for maintaining shared information and state.


### Lesson 1.2 - Consensus Mechanisms
- What are consensus mechanisms?
	- Facilitate the agreement process among participants to guarantee data consistency.
- "The purpose of a consensus algorithm, in general, is to allow for the secure updating of a state according to some specific state transition rules, where the right to perform the state transitions is distributed among some economic set."   - Vitalik Buterin

- Everyone must have the same ledger
- Consensus mechanisms incentivize honesty
- Different approaches
	- Practical Byzantine Fault Tolerance (PBFT)
	- Proof of Work
	- Proof of Stake
- Each mechanism includes rules to determine what is a valid block
- Byzantine Generals problem
- Practical Byzantine fault tolerance 
	- Mathematical verification of messages
	- Tolerates ~1/3 dishonest or absent participants
- A functioning network with 1 out of 4 faulty nodes is byzantine fault tolerant
- Once an agreement is verified, the ledger is then updated

- <u>Rule:</u>
	- Block hash must be less than target number (difficulty)
		- Target = Block Difficulty
	- Miners guess and check hashes
	- Broadcast solutions to the network
	- Solution includes rewards for the miner
	
- <u>POW</u> is a competition for the reward
	- Who can find a valid block hash first?
	- Ethereum: 15 second block time
	- Computationally expensive
		- High energy use
	- Low transaction volume
		- unknown parties
		- Difficult to use a disincentive program to punish bad actors
		- Public blockchains
			- Users' hardware is unknown and can slow the network down
		- Other consensus mechanisms use less energy and can increase the speed and volume of the network

- <u>POS</u>
	- Proof of Stake
	- Currency Holders stake some currency for the chance to determine a block
	- Rule: A block validator is randomly selected by the network
	- Chance of being selected is proportional to their stake in the system
	- Favors large stake holders

- Leased POS
	- Token holders can lease balances to others
	- Rewards split among leasers

- Delegated POS
	- Balance holders elect block validators 
	- No sharing of block rewards

### Lesson 1.3 - Mining in Ethereum
- Proof-Of-Work (POW) is a guessing game with answers that are hard to find, but easy to verify
- Participants guess answers to a problem, looking for a valid solution

- Guessing Game
	- When a correct answer is determined, the discoverer proposes a state update
		- 1. Winners broadcast their solution to the network
		- 2. Participants verify the solution
	- The 'difficulty' of the game changes 
	- If the game is too short, the difficulty increases
	- Ethereum determines a 'difficulty' for the guessing game on the basis of how quickly people have been winning the guessing game on average over the previous interval

- What's in an answer?
	- An answer to the guessing game is called a <u>Block</u>
	- Block contents:
		- A list of transactions
			- Updates the system or State
		- The hash of the most recent guessing game answer
		- A random number called <u>Nonce</u> ("Number used Once")
		- Miner Reward

- Incentive System
	- Because computer '4' guessed the correct answer, they get to add a special command to the block telling other computers to add money to a wallet address that they specified.

- Consensus Rules:
	- 1. Reject invalid blocks
	- 2. Require proof of work (hash < target)
	- 3. Longest chain wins


### Lesson 1.4 - Public and Private Blockchains
- Blockchains can be set up to have different levels of accessibility
	- Public
	- Permissioned/Consortium
	- Private

- Public Blockchains
	- Allows anyone to join as a trust-less participant (pseudo-anonymous transactions)
	- Anyone can read and write data
	- Transaction processors must invest financially to prevent fraud
		- Proof of Work
		- Incentivized by direct economic incentive (cryptocurrency)
		- Costs cryptocurrency to process transactions
		- Censorship Resistent

- Consortium Blockchains
	- Only verified participants are allowed to participate
		- Enables different consensus mechanisms
	- Can achieve higher transaction throughput compared to public networks
	- Example: JPMC has been running a Consortium Blockchain since 2018 for interbank transfers.  It allows them to automate fraud detection/resolution and reduce the amount of time that money is held up from 30 or more days to less than one day.  

- Private Blockchains
	- Designed for rapid application development, instant deployment, and single-enterprise deployment solutions.
	- Best for prototyping and development needs for learning.
	- Participants are know and trusted
		- Legally accountable validators incentivized by reputational risk
	- Potential for a small number of nodes with ability to change data


### Lesson 1.5 - Distributed Ledger Platforms
- Blockchain Platforms
	- Great diversity in the ecosystem
	- Every chain has unique features that make them better suited for different things


### End of Lesson 1
- We covered:
	- Distributed ledgers and how they are different from traditional data architectures
	- Consensus mechanisms and how they enable distributed ledger technology
	- Mining in Ethereum and how it secures the network for Public and Private blockchains
	- Blockchain platforms
