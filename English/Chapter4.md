# 4. Developing an addition game with Klaytn Tools
## 4.1 Intro
 

Hi, everyone. In this tutorial, I will try to develop a BApp called a simple addition game using the Klaytn blockchain. For reference, BApp is an acronym for Blockchain Applications. Let's create a simple, pop-up game that will pay 0.1 Klay for free if you solve the addition problem in 3 seconds.
 
 
Let's look at how it works. First, log in to the operator account. We will verify the account using the keystore file and password combination. So select the keystore file and enter the password. Once the account is verified, use the Send KLAY to Contract button to set the total amount to be used for this event. The reason we send the KLAY to the contract address is to show the user the amount of money to be used for this event in a transparent way. Note that this can only be done with an operator account.


I'm sending it to contract now. I send about 1 KLAY. Once the transaction is completed, the user will be shown the amount to be spent on the event. Like this. Now users can start the addition game. If you set it in 3 seconds, 0.1 KLAY will be sent to user account from contract. Let's get started.
If the solution is wrong while doing this, it will be reset again. If you try again, and if you solve it,  you can get KLAY by pressing the OK button. When the transaction is completed, the balance is reduced by 0.1 in the contract. As you can see, transaction processing is very fast. It’s a strong point Klaytn. If you click on the link below, it will take you to the Klaytn scope where you can see the information of the transaction just created.


If you have experience developing the Ethereum DApp, the upcoming course will be quite easy for you. Klaytn is a platform forked out by Byzantine versions of Ethereum, so you will feel familiar in many ways. For example, the JavaScript library, caver.js, which can communicate with the Klaytn blockchain, is similar to Ethereum’s web3.js. In addition, We support solidity languages ​​most commonly used for smart contract development.


Because it’s using the Truffle framework, you can quickly adapt to the development of BApp. Those who have no experience developing BApp can develop BApp in Klaytn blockchain platform with this exercise. But first of all, it is good to understand the basic blockchain and solidity which is a smart contract development language. I put a link to learn.
Yes, we are going to develop with some tools that support Klaytn,
First, I use an IDE that can test smart development, a wallet that can manage accounts.
and  Klaytn scope, a search engine to find transaction information.

 
 
## 4.2 Klaytn Wallet & account management
 

To use a blockchain network, you have to have your own account. You need a bank account to manage your KLAY tokens. So I'm going to use Wallet from Klaytn. It is user-friendly and very easy to use. https://baobab.klaytnwallet.com/ If you go to this address, you can connect to the Baobab network and create and manage your account. For your reference, this Wallet is for testing purposes, and the Klay used here has no monetary value. First, let's create a new account. Click Create a new wallet. It’s a process that is creating a password and keystore file. Before that, I will explain what the keystore file is. It’s like we are now in the process of going to the bank to make a bankbook, and  put this bankbook in the safe so that others can not use it. This vault is a keystore file and password combination, which protects the secret key required for transaction signing from hackers and external intrusions.


Now, let's continue and create a keystore file. Enter your password here, click next step, and download the keystore file. Downloaded,
Then I will tell my next screen to save my secret key somewhere. The secret key here is an essential requirement for signing a transaction in the Klaytn BApp. This secret key should never be exposed to the outside. It is like going away my bankbook and bankbook passwords and losing all the money.
 


That's why I create a keystore file to protect my secret key. The keystore file and the keystore password must be known before the secret key is accessed. Even if a hacker  gets a keystore file, the secret key is not accessible without password. So the hacker cannot get the money. That does not mean you can easily shed keystore. Do not expose it to the outside.
Now I'll save this secret key in Notepad. You must not do this,, but it is a mere test-net and I will do it for convenience just for now. You can save your private key in the place you feel safe. Once you have saved, click on the view wallet info on the left. Now I can access my wallet. There are two ways to approach it. The first is to use the secret key, and the second is to access the keystore file and password. First, let's access it using the secret key. Copy and paste it in Notepad.

 
My Wallet information is now available. Here is my account public address and my secret key below. I can see my transaction list. I don’t have to deal with this because I have not created a transaction yet. On the right side, I can see how many KLAY I have and I can also add a token to my Wallet by clicking on the plus button.
 
Now let's get KLAY on my account. Click on the KLAY faucet tab to get free klay. My current account address has a zero balance. If you press the Run faucet button, you will receive 5 KLAYs. Once you receive it, you can receive it again in 24 hours. Since you can not get many KLAYs in a short time, you should split KLAY as much as possible when testing. The reason we get it after 24 hours is that some people have been using this KLAY  have been identified with malicious use of KLAY. Klaytn said that they are dealing with fraud, so it'll be better. Now let's transfer the KLAY to another account. 
 
 


If you go to the Send klay & token tab, you can send money from my address to another address. Enter the recipient address. I'm going to send a KLAY in the bottom to decide how much to spend. It says that 0.000625 KLAY will go out with the below transaction fee limit. It’s like paying for a commission fee. How this cost is measured is equal to the gas price multiplied by the gas limit. You can think of the gas price as the money paying for asking transaction to the consensus node. Klaytn's gas price is always fixed, unlike Ethereum. It is difficult to predict the total commission cost because the gas price of the Ethereum is fluctuating. However, Klaytn's gas price is always fixed at 25 ston, no matter what transaction you process.

 

The gas limit is the maximum cost of the gas dealing with this transaction. For example, let's say we have some infinite loop in this transaction we are sending. Then this simple transaction is going to continue running in the network. This causes performance degradation of the network. You should not hurt everyone. So, if you have more than 25,000 gas, Klaytn thinks that something is strange and it stops processing.



And I said the gas price is 25 test_ston, ston is one of the currency units of KLAY. Just like a dollar in the United States is 100 cents, there are many units of KLAY. https://docs.klaytn.com/klaytn/design/computation/exec_model The Klaytn official document shows KLAY units. There are many things. There is a standard KLAY unit in the middle, and the peb at the top is the minimum unit that represents the KLAY. The unit that is used for the 10th round of the peb is ston. So what would be the 25 ston converted to klay? https://blockchains.tools/pebConverter?l=KLAY If you come to this site, you will convert many units. If you put 25 on ston, looks how much KLAY we get. If gas limit 25000 is multiplied by this, 0.000625 KLAY will come out. It is used as a transaction fee. Let's try it with a calculator. If you copy this and multiply it by the calculator gas limit 25000, the transaction cost comes out. This is the cost of processing transactions.


Note that when you send these simple remittances from Klaytn, the transaction cost is always fixed at 0.000625 KLAY. However, the transaction cost is not fixed in the transaction through smart contract function because the gas limit changes according to the complexity of the transaction. I will explain more about this later.
 
You can manually change the price by clicking the Edit button next to it. But I recommend you to proceed with the default setting.
Let's try to send transaction now. On the next page, you'll see information on how much you send to someone and how much the transaction costs will go. Click yes to the question ‘Do you want to continue?’ Then the transaction is completed in a blink of an eye. Then click on view transaction info and the contents we send to you will be saved in the block and shown to the user. I will explain this later in more detail. So far, I've used Klaytn Wallet.

 

## 4.3 Klaytn IDE & Smart Contract 1
 
With the IDE provided by Klaytn, let's create a simple smart contract for our add-on game. Rather than focusing on smart contracts, I'm going to focus on Klaytn tools.
You can create and test smart contracts by visiting http://ide.klaytn.net/. It is similar to Ethereum's remix IDE, but here it is used to connect to the Klaytn node, not to the Ethereum node. Now let's look at the features of the Klaytn IDE by creating our own smart contracts for our add-on games.
 
For reference, a smart contract is called smart contract in English. I’m going to call it ‘Contract’ in my lecture. If you look here, you already have a count contract created by default. I'll erase this and start. Please delete it. And as you can see in the comments at the top, the Klaytn IDE writes the Solidity 0.4.24 version, so you have to proceed with this version.
 
Our contract has three functions. The first is to send the KLAY to the contract, the second to load the balance of the contract, and finally the function to send the KLAY from the contract to the user account. We will make one by one and use the tools to test it. First, let's name the contract as AdditionGame, Contract Edition game.
 
(Code)
At the moment of deployment, you create a state variable that can store the address of the operator account. And I'm creating a constructor. Before that, what does the constructor usually do? Yes. It is primarily responsible for initialization. In the case of solidity, you can not write or load the constructor again, especially since it is the constructor that is first loaded when you deploy. I can take advantage of this and set up an account for the owner of the contract. First, we create the state variable owner. The type is an address type. I'm building a constructor. Owner is msg. Sender.
 
(Code)
I just created a constructor. msg.sender is the person currently calling this contract. Msg.sender in the constructor means the account being used to deploy. So, I will assign that account to the owner state variable and record it to the blockchain forever. This is the initialization. So let's test the code we just added. You need to compile first. Click on the Auto checkbox at the top of the right panel to automatically compile each time you write the code. At first, you have to click on the compile button to see if it compiles. Yes, the compiled information is on the bottom. Let's set the environment again. Environment There are several options to choose from: DEV NODE and Baobab. And I can add a new network. The Add New Network function connects to the RPC address where the Klaytn node is currently running and tests it. I will skip this part for now. Dev node is an option to connect to and test the development node provided by Klaytn. It creates a random account and allows you to pre-order 100 KLAYs. And it's set to run out of gas for testing. So if you see From Account below, there are already 100 test KLAYs in this account. The option to connect to Baobab is also connected to the official test net. And the moment you select Baobab, the KLAY in the account below changes to zero. Dev nodes and baobab nodes operate independently of each other, so accounts at the same address are recognized by each other, but the state of the account is different because the nodes are different. So the balance will change.
 
 
Let's try to refresh the page with the Dev node selected again. Next, to Loading account, there is no account that I used before, and I create another new account. The funny thing is that you can download this account as a separate keystore file or secret key and reuse it. If you are testing on another computer, you may want to continue with the account you used. You can use this option at that time. For example, if you click on an account, you have a backup current account. When you select it, a window opens and you have the option to receive your keystore or secret key. Simply back up your secret key. When you click Copy to clipboard, you have now backed up the secret key for this account.
 
 
Then refresh the page again. Once the account is created, click again and select the import an account option. Go to the Private key tab and paste the backed up secret key. The display label will be called the test account. Import. If you select the account again, you will have the test account we imported below. So when you come back to this page in this way, or on another computer, you can do the test consistently.
 
 
Rather than explaining Tx Value, I will try to deploy it first. Deploy
. After you click the compile button, you have the option to deploy our AdditionGame. Click deploy. Then, deployment was completed in less than 3 seconds. There is a TX hash in the middle panel, right? This is the transactional hash information that was generated by the deployment. On top of that, it shows which address the contract address was deployed to.
 
 
If you look at the panel next to it, you will see which address currently has the contract deployed, and below you have the option to load the value of the owner state variable. This is a getter function. Since we have declared the visibility of the state variable owner public, we can automatically generate a getter function to retrieve the value of the owner variable. When you press the Call button, the address below appears. What is this address then?
 
Yes, this is the account address of the person who deployed this Contract. I have deployed the contract with the account visible in the “from account”, so this account is saved as the value of the state variable owner. Yes, I've written solidity code through the Klaytn IDE and tested the contract owner. Next, we will write and test the remaining two functions in the next class.




 
## 4.4 Klaytn IDE & Smart Contract 2
 

Let's continue to create a function that shows many remaining KLAY balances are in the contract address. Please select the auto checkbox next to it. Inside the constructor, we're going to create a getBalance function.
(Code)

The function keyword is used, the name is ‘getBalance (),’ the visibility is public, and the type is read-only with a view. Finally, define the uint type as a function that returns.
(Code)

address (this) refers to the current contract itself. This is the edition game contract. And accessible the balance as a member. This completes the function to load the KLAY balance at this contract address. Let’s re-deploy it for testing. Click on the Deploy button, then the getBalance () function is created and the Call button is activated. Let's click on this once. Then the current balance is zero. I have not sent anything yet.
 
 
Next, let's create a function that sends KLAY to the contract address from the owner account.
(Code)

I made the visibility public and made the type payable. Whenever you send a KLAY to a solidity function in your account, you must always make the type as payable. That way I can get money from the function. Next, we will check the validity.
 
(Code)

If you do not use the require keyword, the function will be terminated. msg.sender refers to the account that called this function now, and compares that account to the state variable owner account, so that if the account that currently loads this function is not the owner account, it will not execute the function. So I checked the validity check to see if I could transfer the KLAY from the owner account to the contract. Now, let's try testing.
 
 

Please press the Deploy button. The deposit function is now activated. If you send a KLAY with the deposit function, you have to use Tx.value. If the function has a payable type, you have to use tx.value. With test_KLAY next to it, enter 1 as the value. Then click the deposit send button. Your transaction succeeded and returned a transaction receipt. If you look at the account from the ‘from account,’ the balance is reduced from 100 KLAY to 99 KLAY. If this were the original, we would have to deduct the balance, including the cost of gas used to process the transaction, but we have chosen dev node, which does not include the development node or gas bill.
 

Now let's call the getbalance function to see how much the contract's balance is. It contains a value. Please note that we have only sent 1 KLAY, and the number is so large that you may get confused. This is now the value of 1 KLAY converted to peb, the minimum unit of KLAY. In the Klayton virtual machine, you need to convert KLAY to the smallest unit of peb and process it, so you see this number. When typing a value from tx value and sending it to the deposit function, thankfully the IDE will automatically convert it to the smallest unit, peb.
It's a very useful feature for testing. Conversely, you can also test with different units in tx value, this time with the lowest unit, peb. Let's convert 2 KLAYs to peb and send it to the contract. Return to the unit conversion site, enter 2 KLAYs, copy the converted value to peb, and paste it into tx value.
 
 
And then you call the deposit function. The transaction was successful. Let's call the getbalance function. Then the value increased. I've learned that you can test with unit conversion.
 
 

And the gas limit is the limit of gas, which is auto by default. In other words, it calculates the gas limit for entering the function and automatically defines it. This is because the calculation depends on the complexity of the function. So the gas limit for function processing is not fixed. When we send money with a wallet from the former course, the gas limit was fixed at 25000. It's just a transaction that sends money, so there is no complexity and the gas limit is fixed. In fact, you can manually enter this gas limit and try a ㅇㄴmore precise test. So far, I have learned the gas limit, and I have covered the part of transferring money from the owner account using transaction value to contract.
 

 
## 4.5 Klaytn IDE & Smart Contract 3
 

With this last function, let's write a logic to transfer the money in the contract to the user account when the user has solved the problem of the addition game. For reference, the user who answered the correct answer calls this function directly to receive the money.
 
Get a KLAY value to pass to the user as an argument. Note that this value is converted from the front end to peb and passed. And a function that returns a Boolean. Next, you need to validate that the balance in the contract is equal to the value you want to send to the user.
 

Call the getbalance () function above to call up the remaining balance in the current contract and pass it if it is equal to or greater than the value received as an argument.
 

The user with the correct answer has called this function, msg.sender,
(transfer (_value)) to get the prize money and send the KLAY to the user using the transfer function. And finally, I'll return whether it was successful. 
 

Now, we have written the smart contract code that we will use. It was very simple, right? Now let's do the final test. To deploy, set Tx value to 0 and set gas limit back to auto. Your deploy was successful. In order to use the transfer function, we will send the KLAY again because the contract balance is 0 after the new deployment. Tx value is 3 and I’ll change Test_peb into Test_klay. Press send button in deposit function. If the transaction was successful, click ‘get balance’, your money came in. Remember that my account balance is 94 KLAY.
 
Now let's use the transfer function. Set the Tx value back to 0 and click the send button of the transfer function. Now, this is a function that contains parameters, you have to send the argument value when the window comes out. You must also convert the KLAY to peb when you send it. Remember that KLAY values ​​sent to the contract are converted to peb and passed. Go back to the conversion site and convert 1 KLAY. Copy and paste Peb values. Presse the call button and the transaction will be executed and the receipt will be returned successfully. Balance of ‘From account’ has been increased by one more KLAY. It was 94 KLAY just before. Finally, when calling the getbalance function, there are a total of 2 KLAYs left, with 1 KLAY decreased.
 

For reference, this dev node is a node that is actually running, so, the track of the transactions we did will be recorded in the network. How do we test it? All you have to know is the contract address. The information under the deploy button is the contract address we have deployed to the dev node. Copy this and refresh the page.
 

Click the compile button again and click the addition game arrow. Under it, paste the contract address again. Then the functions are activated again. Let's call the Getbalance function. Your balance will remain the same amount as before. It's easy. If you know only the contrack address, you can see the records I have tested. So far, we’ve studied the addition and testing of the addition game using the Klaytn IDE.
