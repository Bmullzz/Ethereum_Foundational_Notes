# Smart Contract Inheritance

## Inheritance Overview

As with many object-oriented languages, Solidity includes **inheritance** as a feature.

Inheritance means that you can create an object with some values/methods and use it as a base for other objects.

In Solidity, the objects we're referring to are _contracts_ and _interfaces_. We can write a contract with state variables and functions. Then we can create contracts that inherit those variables and functions. These derived contracts can then choose to add behavior as necessary.

Smart contracts can inherit other contract by using the `is` keyword. More specifically, a contract that inherits is the **child** and the inheritor is the **parent**. Using the `is` keyword in Solidity establishes a smart contract parent-to-child chain. So whenever you think of inheritance, just think of the infamous father-son duo: Draco and Lucius Malfoy!

## Inheritance in Computer Science

![inheritance flow](image.png)

**Inheritance** allows programmers to create classes that are built upon existing classes, to specify a new implementation while maintaining the same behaviors.

- If you've ever taken a Java 101 course, you'll have seen this concept covered.

As in the illustration above, we start with the **parent class** called `Animal`, which contains some data and has some "base" or "default" behaviors such as `move()` (all or most animals can move!) and `eat()` (all or most animals eat!).

Then we have the **child class** called `Dog` that "inherits" (symbolized by the arrow pointing downward) the `Animal` parent class. A dog `is-a`n animal! A dog has all the base behaviors and data that an animal has (because it `is` an animal).

- Notice the important keyword: `is`

Let's break down all the labels on the illustration:

- **parent class**: `Animal` is the parent class of `Dog` (relative parent! If there is no `Dog` to inherit to, it is simply just a class!)

-  Parent classes are often times also referred to as **base classes**.

- **overriden method**: `move()` is a method that `Dog` inherits but overwrites! 

    - If a method is overriden, that means the child class implements it different. A dog is an animal so it moves, but it moves different to other animals.

- **inherited method**: `eat()` is an inherited method from a non-pictured parent class of `Animal`. Every living being eats. So the the parent class that `Animal` inherits from could be called `LivingBeing`.

- **child class**: also referred to as a **subclass**, this is simply the class inheriting from a parent. This is the Draco to the Lucius Malfoy.

- **overriding method**: as covered three terms up, this is the method that the `Dog` child class inherits but overrides. Dogs move different to all animals!

Keep these core concepts in mind as we study inheritance in Solidity below. These concepts work the **exact same** in Solidity... but instead of classes, just use contracts!

## Inheritance in Solidity

Contracts can **inherit** other contracts by using the `is` keyword.

![inheritance is-a](image-1.png)

Just as illustrated in the diagram above, the syntax to establish inheritance between smart contracts in Solidity is to simply use the `is` keyword in the child contract - which creates an explicit pointer to the parent contract:

```solidity
contract A {
    
}

contract B is A {
    
}
```

In this case `Contract A` is the parent contract, often times referred to as the **base contract** whereas Contract B is the child contract, often referred to as the derived contract. Let's break down the different types of smart contract inheritance in Solidity.

- The term "derives" is one you'll hear a lot! A contract **derives** another contract if it inherits from it. Just like a child derives features from a parent!

## Single Inheritance

![single inheritance](image-2.png)

**Single inheritance** helps in inheriting the variables, functions, modifiers, and events of base contracts into the derived contract. This is the exact same diagram as was introduced above.

## Multi-Level Inheritance

![Multi-level Inheritance](image-3.png)

**Multi-level inheritance** is very similar to single inheritance; however, instead of just a single parent-child relationship, there are multiple levels of parent-child relationships. This is what is referred to as a **smart contract inheritance chain**. In this case, `Contract A` is the base contract as it is the contract all other contracts inherit from.

## Hierarchical Inheritance

![Hierarchal Inheritance](image-4.png)

contracts3

**Hierarchical inheritance** is again similar to simple inheritance. Here, however, a single contract acts as a base contract for multiple derived contracts. `Contract B` and `Contract C`, in this case, act as siblings but are not interconnected in any way other than that.

## Inheritance Use Cases

Now that we've covered smart contract inheritance at a high level, let's dive into some code-specific use cases. Smart contract inheritance is very useful because it allows us to bring in existing code, variables and functions into any contract we write; all we need to do is use the `is` keyword.

- Inheritance is a great way to follow the [DRY (Don't Repeat Yourself)](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) principle of software development! 

## Ownable

Have you heard of [OpenZeppelin](https://www.openzeppelin.com/) before? They are a company that produces industry-standard smart contracts. This means they develop and deploy smart contracts that are so used, audited and stress-tested that they become industry standards.

One such standard contract is `Ownable.sol`. Let's take a look at some parts of it:

```solidity
contract Ownable {
    address owner;
    
    constructor() {
        owner = msg.sender;
    }
    
    modifier onlyOwner() {
        require(msg.sender == owner);
        _;
    }
}
```

- Read the [full documentation on OpenZeppelin Ownable](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable) if you want to explore further into contract access control.

The above `Ownable` contract carries functionality specific to access control of a smart contract. Out of this contract, we get:

- a variable of type `address` called `owner`

- a `constructor` that declares the `owner` is equal to whoever deploys the contract

- a `modifier` that can be placed on functions to make sure only whoever is the current `owner` can proceed

These are all great and very useful functionality! Ready for the magic, fellow Alchemist?

Say you are writing a new kickass smart contract. Let's call it `MyContract` and give it some simplistic functionality, like keeping track of a `uint` state variable:

```solidity
contract MyContract {
    uint public x = 1337;
    
    function changeNumber(uint _x) public {
        x = _x;
    } 
}
```

All right easy enough, it's pretty bare though. And it's not very secure. The `changeNumber()` function is marked `public`, meaning anyone can change our state. We don't want that. We want to implement access control. But wait... at this point, you know about **smart contract inheritance**! Why not just **inherit** the access control functionality from the OpenZeppelin `Ownable` contract we looked at above?! Like so:

```solidity
contract MyContract is Ownable {
    uint public x = 1337;
    
    function changeNumber(uint _x) public onlyOwner {
        x = _x;
    } 
}
```

BOOM. 💥 We successfully inherited from `Ownable`, meaning we are able to access all the variables (`owner` of type `address`, ).

**All inheritance does is LITERALLY copy-paste the code of the parent contract into the child contract. That's it!**

Thanks to `MyContract` inheriting `Ownable`, we now have access to the `onlyOwner` modifier, without needing to write it from scratch.

- Writing from scratch is not bad! But you should know when to rely on battle-tested code and when to write your own.

So you don't need to worry about writing access control functionality from the ground up! You can use a fully audited industry-standard contract to abstract that away from you. THis gives you more time to build the dApp of the future! 

Let's cover a few more use cases...

## Multiple Inheritance

Ok, so your `MyContract` now has the powers of the OpenZeppelin `Ownable`. Cool! What if you were trying to create your very own token?

## Token

Imagine we had a very simple and generic Token contract:

```solidity
contract Token {
    mapping(address => uint) balances;
}
```

This `Token` contract is simple: it just keeps track of the balance of users by an address.

Let's now use that `Token` to create our own token:

```solidity
contract MyToken is Token {
    function mint(uint _amount) public {
        balances[msg.sender] += amount;
    }
}
```

Boom! 💥 Token created! What if we want to add access control checks to `MyToken`? We can do so using also inherit from the same `Ownable` contract we used above!

By using **multiple inheritance**, we can power our `MyToken` with both the generic `Token` AND `Ownable` (and any other contract you want to inherit from!).

```solidity
contract MyToken is Token, Ownable {
    function mint(uint _amount) public onlyOwner {
        balances[msg.sender] += amount;
    }
}
```

Now our `MyToken` inherits the `onlyOwner` modifier from `Ownable` - awesome!

This is what our current contract architecture looks like, thanks to multiple inheritance:

![mulitple inheritance](image-5.png)

## Solidity Inheritance - Function Syntax

### `virtual` Keyword

A function that is going to be _overriden_ by a child contract must be declared as **virtual**:

```solidity
function foo() public pure virtual returns (uint) {
    return 10;
}
```

### `override` Keyword

A function that is going to override a parent function must use the keyword **override**:

```solidity
function foo() public pure override returns (uint) {
    return 15;
}
```

## NFT Use Case

Here's a clear example of an NFT base contract that gets extended via inheritance. In order to **override** functions of a base contract in Solidity, you must use two keywords: `virtual` and `override`, like so:

```solidity
contract NFT is Ownable {
    function transfer(address _recipient) virtual public onlyOwner {
        owner = recipient;
    }
}

contract TimeLockedNFT is NFT {
    uint lastTransfer;
    
    function transfer(address _recipient) override public onlyOwner {
        // cannot transfer if last transfer was within 10 days
        require(lastTransfer < block.timestamp - 10 days);
        owner = _recipient;
        lastTransfer = block.timestamp;
    }
}
```

Notice the use of **`virtual`** on the base function and **`override`** for the new functionality.

## Suggested Reading

- [Solidity and OOP](https://medium.com/coinmonks/solidity-and-object-oriented-programming-oop-191f8deb8316)

- [Solidity by Example - Inheritance](https://solidity-by-example.org/inheritance/)

- [Calling `super` Class](https://ethereum.stackexchange.com/questions/90243/calling-super-class-external-functions)

## Conclusion

The big takeaways for inheritance in Solidity is:

- following the DRY (Don't Repeat Yourself!) principle of software development

- you can always use a _base_ functionality of a contract then customize it with your own features using the `virtual-override` pattern seen above

