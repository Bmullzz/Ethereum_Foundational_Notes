# Contract Puzzles

- [AU Contract Puzzles Repo](https://github.com/ChainShot/Contract-Puzzles)

## Instructions

Today, we will be cloning down some fun smart contract puzzles. In these challenges, you will need to analyze the source code and somehow trigger a `win` condition.

The objective is to set this `isWon` to true **without modifying the smart contract**.

You will need to analyze the source code of five simplified smart contracts and determine how to solve a puzzle for each one. **Once you've figured out the puzzle, modify the test cases to complete the task successfully**.

The way to solve these challenges is: **do it using the relevant contract's test file**! So if you are solving `Game1.sol`, the way to do it is to:

1. edit the `game1Test.js` file

2. leave the `Game1.sol` contract intact

3. run `npx hardhat test test/game1Test.js`

    - You can run all the `test` files in the test folder by running `npx hardhat test`

## Set Up Project Locally

1. In a directory of your choice, run `git clone https://github.com/ChainShot/Contract-Puzzles`

2. Run `npm install`

3. Read the [README.md](https://github.com/ChainShot/Contract-Puzzles/blob/master/readme.md)

4. Once you are able to `run npx hardhat test` and get all the tests passing green with ✅✅✅✅✅ check marks, you have successfully solved all the challenges!