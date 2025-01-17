---
id: local-dev-node
title: Local Development on Local Node
sidebar_label: Local Development on Local Node
---

## Requirements

**IMPORTANT: Make sure you have the latest version of NEAR Shell and Node Version &gt; 10.x** 

* `npm` \(Get it [here](https://www.npmjs.com/get-npm)\)
* `node version 10.x`\(Get it [here](https://nodejs.org/en/download)\)
* `near-shell`  The NEAR cli tool.
  * Install with`npm i -g near-shell`
  * Check out the commands [here](https://github.com/nearprotocol/near-shell)

**Docker**

* By default we use Docker to run the client:
* [MacOS](https://docs.docker.com/docker-for-mac/install/)
* [Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

## 1. **Run a node locally**

For this step, please refer to the documentation on [running a node on testnet](../local-setup/local-dev-testnet.md) (Linux/MacOS) or the documentation on [running a node on Windows](../local-setup/local-dev-testnet.md). Follow the steps and once your node is running come back to this part of the docs for step 2.

## 2. Create an account and start the node

You will then be prompted for an Account ID. An account will be created for you, which you can then use to deploy your contracts. **It is important that you enter an account ID here so that an account is created for you. Ignore the 'leave empty if not going to be a validator' message.'**

```
Enter your account ID (leave empty if not going to be a validator):
```

A node will then start in the background inside the docker. To check the logs inside the docker, run `docker logs --follow nearcore`.

You should see the success message `Node is running!`

run `docker logs --follow nearcore` to see the logs. 

## 3. Create a new project

Highly recommand see the package [here](https://www.npmjs.com/package/create-near-app) to get details 

In command line, run different command to build different blank project:

React JS app:
```bash
npx create-near-app path/to/your/new-awesome-app
```
Plain app:
```bash
npx create-near-app --vanilla(--plain) path/to/your/new-awesome-app
```


Then go to your project and follow README.md in it.


## 4. Write the smart contract

Your project is pre-seeded with a simple contract which you can deploy right away, so feel free to head to step 5.

If you've already successfully deployed a contract, you'll probably want to start coding your own smart contract. If so, you'll find the below resources helpful.

* [Wrtiting Smart Contracts](../development/writing-smart-contracts.md)
* [Calling Smart Contracts](../development/calling-smart-contracts.md)

For a deep dive into the file structure of a NEAR Project template, take a look here:

[NEAR Smart Contract Development Overview](../quick-start/development-overview.md)

## 5. Create an account for your contract on the Local Node

Let's now deploy your contract to the local Node which you have running.

You'll first want to specify NODE\_ENV to be 'local.' Set the NODE\_ENV constant by running this command in bash: 

`export NODE_ENV='local'`

From there, use this command to create an account for your contract

```bash
near create_account <yourcontractname> --masterAccount=<login> --initialBalance <initalbalance>
```

**--masterAccount= :** specifies which account's key should be used to deploy the contract. Should be the same account that you created when running the Local Node; i.e. this is your username.  
**--initialBalance :** specifies how much to seed the contract balance with; e.g. 100000

You should see the success message: 

`Account <yourcontractname> for network "default" was created.`

The last step is now to update the src/config.js to use &lt;yourcontractname&gt; for deploy. 

```javascript
(function() {
    const CONTRACT_NAME = '<yourcontractname>'; /* TODO: fill this in! */
    const DEFAULT_ENV = 'development';
    ...
})();
```

## 5. Deploy your contract and start the web server

Deploy your contract to TestNet and start web server for the frontend.

```bash
npm run start
```

You can run `npm run start` each time you want to redeploy the updated smart contract, or to restart your web server.

For help using cli tools, use `near`. To get a list of available `npm` scripts use `npm run`.

