
# Super Loto Number Generator

A small gadget that creates 6 numbers (1-60) for every demand of the user. The user are welcomed for donation in Near token.



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

---------------------------------------------------------------------------
## playGame 

 - Takes ***_gameId*** and ***_guess*** as parameters
 - Guess must be between 1-6
 - The game's player and the person calling the function must be the same
 - A game has to be in the **JOINED** state in order to be played
 - returns the dice number as well as the winner's name
 
**Example call:**
`near call $CONTRACT playGame '{"_gameId":'$GAMEID' , "_guess":3 }' --accountId $NEAR_ACCOUNT`

## deleteGame 

 - Takes ***_gameId*** as  a parameters
 - The person calling this function must be the owner 
 - The game must be in the **FINISHED** in order to be deleted
 - returns a string confirming game deletion

 **Example call:**
`near call $CONTRACT deleteGame '{"_gameId":'$GAMEID' }' --accountId $NEAR_ACCOUNT`
 
## viewGame 
 - Takes ***_gameId*** as  a parameters
 - returns the game's details
 
 **Example call:**
`near call $CONTRACT viewGame '{"_gameId":'$GAMEID' }' --accountId $NEAR_ACCOUNT`
 
## viewAllGames 
 - Does not take anything as a parameter
 - returns an array of all games

**Example call:** 
`near view $CONTRACT viewAllGames --accountId $NEAR_ACCOUNT`

## reactivateGame 
 - Takes ***_gameId*** as  a parameters
 - The person calling this function must be the owner 
 - The game must be in the **FINISHED** in order to be reactivated
 - The creator must attach some tokens into the function
 - Returns a string confirming game reactivation

**Example call:**

`near call $CONTRACT reactivateGame '{"_gameId": '$GAMEID'}' --amount 3 --accountId $NEAR_ACCOUNT`


# Front-end
The front-end for this project was build using NextJS as a framework.

In order to run the front-end locally you have to run the command:

    yarn dev

 

## Linking front-end to the contract
The front-end is linked to the 	***dice.aimensh.testnet*** contract by default ,  if you want to connect your own contract with the front-end, you need to replace the **CONTRACT_ID** variable in the ***near/near-setup.js*** file with your own contract id.

    export  const  CONTRACT_ID = "CONTRACT_IDs";

