# Guide
## Set Up Your Local Environment
This guide describes how to set up your environment using a specific toolset: Node.js + npm + hardhat. It also shows you how to use the NEST contracts, which are required for the contract examples in the NEST Docs guides.

### Create a Node.js Project
1. Download and install Node.js and npm.
2. Create a new directory and navigate to it. Also, create a new node project with npm init.

### Install Hardhat
1. Install Hardhat, a development environment to compile, deploy, test, and debug your Smart Contracts.

```
$ npm add --save-dev hardhat
```

2. Create a new hardhat config file, which you can use for compiling and testing contracts. For an example of how a typical smart contract repo is structure, select the "create a sample project" option during setup.

```
$ npx hardhat
```

### Set the Solidity Version for Hardhat
For this example, we'll need to change ./hardhat.config.js to include the appropriate solidity version for compiling the NEST contracts. If you are using Hardhat's example project, you can skip this step.

```
module.exports = {
  solidity: '0.8.9',
}
```

### Compile Your Contracts
```
$ npx hardhat compile
```
If everything worked correctly, and you used hardhat's simple example project, you should see the following output:
```
Downloading compiler 0.8.4
Compiled 2 Solidity files successfully
✨  Done in 3.25s.
```
