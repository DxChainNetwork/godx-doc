# Go DxChain DPOS Tutorial

- [Go DxChain DPOS Tutorial](#go-dxchain-dpos-tutorial)
  - [Section One: Introduction to DPOS Roles](#section-one-introduction-to-dpos-roles)
  - [Validator](#validator)
  - [Candidate](#candidate)
  - [Delegator](#delegator)
  - [Section Two: Delegator Tutorial](#section-two-delegator-tutorial)
    - [Step2.1 Get Candidate List](#step21-get-candidate-list)
    - [Step2.2 Check Candidate Information](#step22-check-candidate-information)
    - [Step2.3 Vote](#step23-vote)
    - [Step2.4 Cancel Vote](#step24-cancel-vote)
  - [Section Three: Candidate Tutorial](#section-three-candidate-tutorial)
    - [Step3.1. Apply for Candidate](#step31-apply-for-candidate)
    - [Step3.2. Start Mining](#step32-start-mining)
    - [Step3.3. Check Candidate List](#step33-check-candidate-list)
    - [Step3.4. Candidate Cancellation](#step34-candidate-cancellation)


## Section One: Introduction to DPOS Roles

## Validator
* There are total of 21 validators in the entire network.
* Validators are elected from a list of candidates.
* Validators are in charge of validating the transactions and producing blocks.

## Candidate
* Candidate gets votes from delegator and compete with each other to become a validator. 
* The more votes a candidate gets, the higher chance it can be elected as validator.
* To become a candidate, 10000 DX token must be deposited.
* Tokens deposited by the candidate also count as its votes.
* Candidate must specify the reward distribution rule, so when candidate became validator, the block reward will be distributed among nodes which voted it.

## Delegator
* Delegator votes for validators who can perform mining operation.
* Anyone that owns DX token can become a delegator.
* Delegator votes candidate by deposit DX tokens.
* The maximum amount of candidates that a delegator can vote is 30.


## Section Two: Delegator Tutorial

### Step2.1 Get Candidate List

You have to check the candidate information before voting. To get detailed candidate information, you must know the candidate list first. Typing the following command in the console to retrieve candidate list:

```shell
> dpos.candidates()
```

### Step2.2 Check Candidate Information

Choose one candidate from the list above, then type the following command to retrieve its detailed information:

> NOTE: replace CANDIDATE_ADDRESS with one of the candidate addresses you retrieved from the previous step

```shell
> dpos.candidate("CANDIDATE_ADDRESS")
```

### Step2.3 Vote

To vote for the candidates you desired, type the following command in the console. By using the command below, you will vote for a list of candidates by depositing 2 DX token.

> NOTE: replace CANDIDATE_ADDRESSES with a list of candidates addresses you want to vote, seperate them by comma. The max amount of candidates you can vote is 30.

```shell
> dpos.vote({from:eth.accounts[0], candidates:"CANDIDATE_ADDRESSES",deposit:"2dx"})
```

### Step2.4 Cancel Vote

To get back your vote deposit, you must send the cancel vote transaction. Typing the following command in the console. Once the transaction is processed, you votes will be invalid, and the vote deposit will be returned in two days.

```shell
> dpos.vote(eth.accounts[0])
```

## Section Three: Candidate Tutorial

### Step3.1. Apply for Candidate

To apply for the candidate, you must specify the deposit you are willing to put and the ratio for distributing the reward. By typing the following command, you will deposit 10000 DX token, and for each block reward you received, 50% of it will be distributed among delegators who voted for you and yourself.

```shell
> dpos.applyCandidate({ratio:"50",deposit:"10000dx"})
```

### Step3.2. Start Mining

Once you applied for candidate, start the mining directly by typing the following command:

> Note: you will not be able to mine any block unless you became a validator. It is just safe for you to start mining earlier because at the time you became a validator, mining operation will be performed automatically so you will not miss any block.

```shell
> miner.start()
```

### Step3.3. Check Candidate List

Wait about 10 seconds for candidate apply transaction to be processed, then type the following command in the console to check if you are in the candidate list.

```shell
> dpos.candidates()
```

### Step3.4. Candidate Cancellation

To get back your candidate deposit, you must quit on being a candidate. Type the following command in the console to send transaction for cancelling candidate:

> NOTE: your deposit will be returned in two days

```shell
> dpos.cancelCandidate(eth.accounts[0])
```
