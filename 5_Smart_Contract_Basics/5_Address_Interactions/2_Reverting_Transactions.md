# Reverting Transactions

What does it mean to revert a transaction?

At the lowest level, `REVERT` is an opcode in the Ethereum Virtual Machine. This means it's a native feature of the VM which we can use through some of the Solidity keywords `revert`, `require` and `assert`.

Let's first talk about what it means to revert a transaction. When you revert a transaction, you essentially make it like the transaction never happened. You halt the execution of the transaction and you remove all state changes. The transaction can still be included in a block, and when it is, the transaction sender will still have to pay for the gas used.

- Technically, **message calls** can be reverted and caught in the contract making the message call (the `msg.sender`). You won't see this used too often, but this is what `try`/`catch` is for in Solidity (see the [docs here](https://docs.soliditylang.org/en/v0.8.17/control-structures.html?highlight=try%20catch#try-catch)).

## Real World Example

Let's take a look at a recently reverted transaction here: https://etherscan.io/tx/0x6def53bf56c2eb9dc08c6b87eeaadf90c46c0f4a57aab5ce9ca1481e7ff690d5

If you look at the error message, it is an error that is coming from Uniswap saying `UniswapV2Router: INSUFFICIENT_OUTPUT_AMOUNT'`. Often times, when interacting with a decentralized exchange like Uniswap, the conditions will change between when the EOA signs the transaction and when the transaction is included in the block. It's perfectly possible that when the EOA signed this transaction, the conditions of the market would have allowed for this transaction to happen, however at the time when it was included in the block it failed one of Uniswap's checks.

You'll notice that there still was an associated gas fee, since this transaction did run in an Ethereum block up until that point of the revert. Since this transaction reverted, the state changes did not go through and no token balances were updated for the user.

## Try It Out

Let's learn to revert transactions inside of smart contracts by learning the syntax ourselves! We have some code exercises for you coming up next.