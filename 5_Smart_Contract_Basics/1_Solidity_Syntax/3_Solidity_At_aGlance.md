# Smart Contracts

Before we dive into Solidity Coding Tutorials, let's study a Smart Contract!

Here is an example smart contract called **OnOffSwitch** written in Solidity:

```solidity
/* Here we specify the solidity versions
 * Any version greater than or equal to 0.6.2
 * or less than 0.7.0 will compile this contract */
pragma solidity ^0.6.2;

contract OnOffSwitch {
    // the switch is on if true
    bool private isOn;

    constructor() public {
        // we'll default to being on
        isOn = true;
    }

    // a publicly accessible function to "flip" the switch
    function toggle() public returns(bool) {
        // flip isOn from true->false or false->true
        isOn = !isOn;
        // return the new value
        return isOn;
    }
}
```

Coming from learning JavaScript, what are some of the immediately noticeable things about this programming language? 

First let's look at the **similarities** to JavaScript:

- Comments appear to be the same! Both syntaxes: `// comment` and `/* comment */`

- The casing used is the same as JavaScript, it is lowerCamelCase

- Curly Braces `{}` seem to serve a similar purpose: marking scope

- Boolean values `true`/`false` which can be modified with boolean operators like: `!`

- The `contract` keyword seems a bit like JavaScript `class`, especially the constructor

- The function syntax looks a bit similar to JavaScript

- The `return` keyword is still used for passing a value back from a function

Now let's look at the **dissimilarities**:

- There seems to be some kind of version control statement at the top: **pragma**

- There are public/private keywords for variables and functions

- The `isOn` variable is prefaced with its type `bool`

- The code refers to the `isOn` member variable without using `this`

- The function `toggle` defines what it will return, a `bool`

Ok, well that was a good quick glance! 

Now let's dive into all of these things we noticed to learn more about the language.

## Compiler Version Control

Version Control can be very helpful to specify a range of versions that are acceptable for a dependency or a tool.

In Solidity, we can specify what versions of the compiler our contract will work with using the `pragma` keyword:

```solidity
pragma solidity ^0.6.2;
```

The `^` symbol indicates that this contract will compile with not only version `0.6.2`, but also anything above that version all the way up until the next minor version `0.7.0`.

This syntax may look very similar to you from **npm** when we worked with the **package.json**! Both of these systems use [semantic versioning](https://semver.org/) where there are three values:

- The **major** version: `x.0.0`
- The **minor** version: `0.x.0`
- The **patch** version: `0.0.x`

**Major** updates make no guarantee of backwards compatibility. Generally major updates introduce **many breaking changes** that will require you to make changes to your code to update successfully.

**Minor** version updates will generally add functionality in a backwards-compatible way.

**Patch** version updates are meant for bugfixes and should not break your code's expected behavior (unless you were depending on behavior which was the result of a bug).

-  It should be noted that, at the time of writing, **Solidity has yet to release its first major version**. Prior to the **major version 1.0.0**, many systems are considered _unstable_ where _anything_ may change at any time. So far Solidity development has stuck to making breaking changes on the **minor** version updates. That is, for example, contracts written for `0.4.x` may not work with solidity compiler versions `0.5.x` and above. Each release will [document the breaking changes](https://solidity.readthedocs.io/en/v0.6.2/050-breaking-changes.html).

## The Contract

At first glance, the `contract` keyword looks a bit like `class` in JavaScript!

```solidity
contract OnOffSwitch {
    // the switch is on if true
    bool private isOn;

    constructor() public {
        // we'll default to being on
        isOn = true;
    }
}
```

Here we are declaring `isOn` as a member variable of the `OnOffSwitch` contract. In Solidity these variables are generally referred to as **state variables**.

Just like in JavaScript classes, the constructor is run _only once_. For contracts, the constructor is run _when it is deployed_. The `isOn` state variable will be set to `true` on the deployment of this contract.

The `isOn` variable is accessible anywhere in this contract by name. Unlike JavaScript class variables, there is no need to use `this`. inside of the contract itself to gain access to the state variables.

- The `this` keyword is still used in Solidity as a reference to the **contract account**. We'll talk about this a bit more in the upcoming coding tutorials!

Since state variables are referred to by name, you may often see constructor arguments using underscores to disambiguate:

```solidity
constructor(bool _isOn) public {
    // in this case we'll accept a boolean argument
    // that will set the initial value of isOn
    isOn = _isOn;
}
```

It's important to recognize that when we make a change to a state variable on a deployed smart contract, we are **modifying permanent storage** on the blockchain.

- Remember from our lessons on Ethereum that permanent storage on the blockchain is stored in Patricia Merkle Tries on every Ethereum Full Node.

Local variables defined inside of a code block `{}` or passed in as arguments live in memory only for the length of their particular scope.

## Control Structures

As you may have noticed in our initial example, Solidity also has the `return` statement for passing back values from a function.

One difference in Solidity is that multiple values can be returned from a Solidity function as a **tuple**:

```solidity
function getValues() public pure returns (int, bool) {
    return (49, true);
}
```

The following statement is perfectly valid in Solidity. Similarly, tuples can be used to **destructure** assignments similar to destructuring in JavaScript:

```javascript
(bool x, bool y) = (true, false);
```

- You can think of a **tuple** simply as a group of values in parenthesis. They are not a formal structure in Solidity so they are primarily used for returning and destructuring as shown above.

Along with the `return` keyword, Solidity also has `if`, `else`, `while`, `do`, `for`, `break`, and `continue` with the same semantics as JavaScript.

## Visibility

You may have noticed the keywords `public` and `private` in the initial contract example shown. These keywords are called **visibility specifiers** because they determine from where functions can be accessed.

As you might expect, a `public` function is one that can be accessed from anywhere. A `private` function is one that cannot be. When a variable is declared `public`, a **getter** function is generated that will allow access to the variable state.

- The keyword private does not **protect the privacy of the data itself**. Any data committed to the Ethereum blockchain is public for anyone to see! Marking it as **private** will simply disallow any other contract from reading or modifying the information.

In addition to `public` and `private`, there are also `internal` and `external` visibility specifiers. We'll discuss these specifiers further as we dive into contract communication through message passing.

## Static Typing

The last big distinction we noticed from the example is that Solidity has **static typing**.

In JavaScript, you don't need to specify the data type. We use keywords like `var`, `let` and `const` that could hold numbers, strings, and other various objects:

```javascript
let strangeValue = 3;

strangeValue = "now im a string!";
```

Changing a variable's type like this may not be the best practice, however from the JavaScript language's perspective this is perfectly valid! This is because JavaScript is a **dynamically typed language**.

In Solidity, all variables must declare their type:

```solidity
bool isOn = true;
```

 Here our `isOn` variable is a boolean value. It must always be `true` or `false`.

 - By default, boolean values are `false`.

 What if we tried storing a number in a `bool`?

 ```solidity
bool myNumber = 10; // ...hmm?
 ```

 No good!. In fact, Solidity won't even compile with a statement like this. 

 The compiler will raise a "**TypeError: Type int_const 10 is not implicitly convertible to expected type bool**." And rightly so! 

 - An exception raised at compile time is called a **compile-time exception**. This means that the compiler was unable to generate bytecode from the program, so we would not even be able to deploy this contract! This is opposed to a **run-time exception** which would happen when someone tried to interact with a contract on the blockchain in some expected way. The exception would occur when a miner tries to validate the transaction. Unless the exception is caught, the transaction will fail and the miner will consume all the gas. 

Static typing also affects the way the a function is declared. Let's use our example above where we returned a **tuple**:

```solidity
function getValues() public pure returns (int, bool) {
    return (49, true);
}
```

 Here the function must declare what type of values it is going to return. It defines that an integer and boolean will be returned in a tuple list in that order.

 If it were to try and return values of a different data type it would throw an exception.

 ## Wrap Up

 In this article we went over some of the basic differences and similarities between Solidity and JavaScript!

 We talked about **version control**, **contract structure**, **control structures**, **scoping**, **access control** and **static typing**. 

 