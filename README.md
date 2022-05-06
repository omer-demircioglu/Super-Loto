
# Super Loto Number Generator

A small gadget that creates 6 number (1-60) rows for a super lotto lottery game for every user's demand. The users are welcome to donate in Near token.

[![Super Loto Demo](loom gif)](loomlink)


# Cloning the project
After cloning the project please run 

    yarn
in order to install all of the necessary packages for the project to run correctly.

## Building and Deploying the contract
The contract is located in under the ***contract/assembly*** folders, after editing the contract you can run

    yarn build-contract
in order to build the contract and get the ***.wasm*** file , if you want to build and deploy the contract at the same time, you can run 

    yarn deploy-contract
This will create a test account and deploy the contract into it.

after the contract is deployed, it is necessary to run the following command in the terminal in order to be able to run the contract


    export CONTRACT=ACCOUNT_ID
where the **ACCOUNT_ID** will be returned after the contract deployment

## Running the contract

**Running contract in the terminal**
If you want to run the contract in the terminal you can either:

 1. Run the `yarn run-contract` which will run a bash file that allows the user to create a session, joining it and getting the numbers.
 Before running this command, **{NEAR_ACCOUNT}** placeholders must be replaced with correct Near accounts (one for who demands the numbers)
 
 2. You can call the contract manually in the terminal , examples are shown below in the functions section.
 

# Functions
## initSession

 - Does not take any parameters.
 - Creator of the session gives a donation > She or he should put at least 0 in order to create a session
 - returns a **session id**

**Example call:**
`near call $CONTRACT initSession --amount 5 --account_id $NEAR_ACCOUNT`

## generateRows 

 - Takes ***_sessionId*** and ***_rowNumber*** as parameters
 - Row number must be between 1-10
 - returns the rows that each consist of 6 randomly generated numbers between 1-60 (inclusive)
 
**Example call:**
`near call $CONTRACT generateRows '{"_sessionId":'$SESSIONID' , "_rowNumber":3 }' --accountId $NEAR_ACCOUNT`



