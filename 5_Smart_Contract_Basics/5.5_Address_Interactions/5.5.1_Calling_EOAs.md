# Calling EOAs

Let's talk about how to use addresses in Solidity!

First off, a bit of review. What are the two types of accounts in Solidity?

1. **Externally Owned Accounts** - All transactions originate from an EOA, they are controlled by a private key which signs off on the transaction.

2. **Smart Contract** - This is code deployed to the blockchain. It is programmed to respond to different inputs sent by EOAs or other contracts.

OK, great! Let's focus on calling EOAs first.

## EOAs in a Smart Contract

Let's imagine we have two authors of a smart contract:

```solidity
contract SpecialNumber {
    address author1;
    address author2;
}
```

What's something we can do with EOAs? We can pay them! Let's do that. Any time this contract receives ether, let's send half to `author1` and half to `author2`.

```solidity
contract SpecialNumber {
    address author1;
    address author2;

    receive() external payable {
        // msg.value is passed to this contract
        uint totalValue = msg.value;

        // make a call to author1 sending half of the ether
        (bool success1, ) = author1.call{ value: totalValue / 2 }("");
        require(success1);

        // make a call to author2 sending half of the ether
        (bool success2, ) = author2.call{ value: totalValue / 2 }("");
        require(success2);
    }
}
```

A [payable function](https://docs.alchemy.com/docs/solidity-payable-functions) is one that can receive ether. The `receive` function is a special function that will be invoked when a smart contract receives ether. We'll touch on this further later on.

Let's take a look at that call syntax, specifically:

```solidity
(bool success1, ) = author1.call{ value: totalValue / 2 }("");
require(success1);
```

What is happening in these two lines? Let's break this syntax up into four parts:

1. The `.call` method

2. The curly brace `{}` syntax

3. The empty string argument passed in `("")`

4. The return value `(bool success1, )`

## Call

First let's talk about `call`. The call method is something you'll find on every address type when you want to send input data or ether to an address. When you do this, you'll be making something called a **message call**. You'll often hear this terminology used to describe a call to a smart contract. We differentiate this from a transaction, which is object signed by the EOA sent to the blockchain.

- In Solidity you'll have access to two relevant globals: `msg` which refers to the **message** describe above and `tx` which refers to the original transaction sent by the EOA. You can see this `msg` being used in the `receive` function above to get the total ether value passed in, specifically the ether amount is the `msg.value`.

## Curly Braces

The curly braces which comes after call `{}` provides an opportunity to override the `value` and `gas` parameters on the message call. The `gas` parameter will be relevant when we start calling smart contract addresses. When you leave it unspecified it will forward along all the gas remaining that the transaction sender designated (through the `gasLimit` parameter on the front-end, remember?).

## The Empty String Argument

You can see where passing in an empty string here. If you were trying to target a function on a smart contract this is where your calldata would go. The calldata will specify the function you're trying to call as well as the arguments you are sending. In this case, we're just trying to send ether to an EOA, so we pass an `""` to indicate there is no calldata.

## Return Value

The `(bool success1, )` part probably looks a bit confusing! Remember how in the previous lesson we wrote a contract that can return multiple values? The call method returns multiple values. Solidity will warn you if you don't use the first value returned, which indicates if the message call was successful or not. In most cases, we will want the transaction to fail if a message call fails. The code `require(success1)` will do just that. We'll take about `require` further very shortly!

In the meantime, let's get some practice on our solidity `address` type. Jump into the next coding lesson to begin!