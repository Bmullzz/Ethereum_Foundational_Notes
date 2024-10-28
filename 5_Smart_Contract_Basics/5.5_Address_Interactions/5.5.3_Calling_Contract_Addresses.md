# Calling Contract Addresses

Okay, so we have taken a look at sending ether to externally owned accounts through the call method. What's next?

Now it's time to send **data** to smart contracts using the call method. Let's take a look at what this looks like:

```solidity
import "hardhat/console.sol";

contract A {
    function setValueOnB(address b) external {
        (bool s, ) = b.call(abi.encodeWithSignature("storeValue(uint256)", 22));
        require(s);
    }
}

contract B {
    uint x;

    function storeValue(uint256 _x) external {
        x = _x;
        console.log(x); // 22
    }
}
```

In the above case we're going to call the contract B with calldata that we manually encoded ourselves with `abi.encodeWithSignature`. This will create calldata in the same format as the data field we encoded in the transaction through ethers.js.

This method can be extremely useful when we need to manually encode calldata like this, however it's not always necessary! In this example we could have just used the definition of the contract B to make much cleaner. Let's take a look at an example below:

```solidity
import "hardhat/console.sol";

contract A {
    function setValueOnB(address b) external {
        B(b).storeValue(22);
    }
}

contract B {
    uint x;

    function storeValue(uint256 _x) external {
        x = _x;
        console.log(x); // 22
    }
}
```

There! Doesn't that look much cleaner? 

Please compare these first two examples. It's important to recognize that they're doing the same thing! Underneath the hood we are making a message call from contract A to contract B passing along calldata to target the `storeValue` function. In the case of this second example, all of that is done for us by using the contract definition of B so Solidity knows how to encode the calldata for us! Super helpful.

Ok here's the last example, and then we'll get to coding! What if you didn't have access to the contract B definition in the previous example? In that case you could use something called an **interface**. Let's see what that would look like:

```solidity
interface B {
    function storeValue(uint256) external;
}

contract A {
    function setValueOnB(address b) external {
        B(b).storeValue(22);
    }
}
```

From contract A's perspective, this code functions the exact same way as before. For the definition of an interface, we only need to give Solidity enough information to figure out how to encode the calldata to call the address `b`. From contract A's perspective, we don't need the full method definition of `storeValue`, we simply need to describe how we'd like to interface with contract B. Make sense?