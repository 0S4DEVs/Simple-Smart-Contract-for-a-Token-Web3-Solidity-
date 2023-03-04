# Simple-Smart-Contract-for-a-Token-Web3-Solidity-
This project is a simple smart contract written in Solidity that creates a token with a fixed supply and allows users to transfer the token between each other.

Project Title: Simple Smart Contract for a Token

Description: This project is a simple smart contract written in Solidity that creates a token with a fixed supply and allows users to transfer the token between each other.

Prerequisites: You will need to have a basic understanding of Solidity and the Web3 framework.

Instructions:

Set up the development environment
Install Node.js and npm (Node Package Manager) if you don't already have them installed.
Install the Web3 framework by running the following command in your terminal: npm install web3
Create the smart contract file
Create a new file called "Token.sol" and paste the following code:
typescript
Copy code
pragma solidity ^0.8.0;

contract Token {
    string public name = "My Token";
    string public symbol = "MTK";
    uint256 public totalSupply = 1000000;

    mapping(address => uint256) public balanceOf;

    constructor() {
        balanceOf[msg.sender] = totalSupply;
    }

    function transfer(address _to, uint256 _value) public returns (bool success) {
        require(balanceOf[msg.sender] >= _value);
        balanceOf[msg.sender] -= _value;
        balanceOf[_to] += _value;
        return true;
    }
}
Compile the smart contract
Compile the smart contract by running the following command in your terminal: solc Token.sol --bin --abi --optimize -o ./build/
This will generate two files in the "build" directory: "Token.bin" (the compiled bytecode of the smart contract) and "Token.abi" (the application binary interface).
Deploy the smart contract
Open the Web3 console by running the following command in your terminal: node
Import the Web3 framework and connect to the local blockchain network:
javascript
Copy code
const Web3 = require('web3');
const web3 = new Web3('http://localhost:8545'); // Change the URL to match your local network
Import the compiled smart contract:
javascript
Copy code
const tokenABI = require('./build/Token.abi');
const tokenBytecode = require('./build/Token.bin');
Deploy the smart contract:
javascript
Copy code
const token = new web3.eth.Contract(tokenABI);
token.deploy({data: tokenBytecode, arguments: []}).send({
    from: '0xYourAddress', // Change to your own address
    gas: 1500000,
    gasPrice: '30000000000' // 30 Gwei
}).then((newContractInstance) => {
    console.log('Contract deployed at address:', newContractInstance.options.address);
});
Make sure to replace '0xYourAddress' with your own Ethereum address.
Interact with the smart contract
You can now interact with the smart contract using the Web3 framework. For example, to transfer tokens from one address to another, you can use the following code:
javascript
Copy code
const tokenAddress = '0xContractAddress'; // Replace with the address of your deployed contract
const token = new web3.eth.Contract(tokenABI, tokenAddress);

token.methods.transfer('0xRecipientAddress', 1000).send({from: '0xYourAddress'}).then((result) => {
    console.log(result);
});
Make sure to replace '0xContractAddress', '0xRecipientAddress', and '0xYourAddress' with the appropriate addresses.

Documentation:

You can find more information on Solidity and Web3 development in the following resources:

Solidity documentation: https://solidity.readthedocs.io/en/latest/

Simple Voting Application
This is a simple voting application built on the Ethereum blockchain using Solidity. The contract allows users to create a poll with a question and a list of options, and then vote for their preferred option. Each user can only vote once per poll.

Installation
To run this application, you will need to have the following software installed:

Node.js
Truffle
Once you have installed these dependencies, you can clone this repository and install the project's dependencies by running:

Copy code
npm install
Usage
To deploy the smart contract, run the following command:

Copy code
truffle migrate
This will compile the contract and deploy it to your local Ethereum blockchain. Note that you will need to have a local blockchain running in order to do this - you can use something like Ganache to set one up.

To interact with the contract, you can use the Truffle console. Start the console by running:

javascript
Copy code
truffle console
Once you're in the console, you can interact with the contract as follows:

csharp
Copy code
// Create a new poll
let poll = await VotingApp.new("What is your favorite color?", ["Red", "Green", "Blue"]);

// Vote for an option
await poll.vote(1, { from: accounts[0] });

// Get the winning option
let winningOption = await poll.getWinningOption();
console.log("The winning option is: " + winningOption);
Testing
This project includes a suite of tests written in JavaScript using the Mocha testing framework. To run the tests, simply run:

bash
Copy code
truffle test
Contributing
Pull requests are welcome! If you would like to contribute to this project, please fork the repository and create a new branch for your changes. When you're ready, submit a pull request and we'll review your changes.

License
This project is licensed under the MIT license. See LICENSE.md for more details.
