# Go DxChain DPOS Tutorial

- [Go DxChain DPOS Tutorial](#go-dxchain-dpos-tutorial)
  - [Section One: Delegator Tutorial](#section-one-delegator-tutorial)
    - [Step1.1 Get Candidate List](#step11-get-candidate-list)
    - [Step1.2 Check Candidate Information](#step12-check-candidate-information)
    - [Step1.3 Vote](#step13-vote)
    - [Step1.4 Cancel Vote](#step14-cancel-vote)
  - [Section Two: Candidate Tutorial](#section-two-candidate-tutorial)
    - [Step2.1. Apply for Candidate](#step21-apply-for-candidate)
    - [Step2.2. Start Mining](#step22-start-mining)
    - [Step2.3. Check Candidate List](#step23-check-candidate-list)
    - [Step2.4. Candidate Cancellation](#step24-candidate-cancellation)

## Section One: Delegator Tutorial

**Delegator Introduction:**
* Delegator votes for validators who can perform mining operation. 
* Anyone can become a delegator by depositing DX tokens to vote for validators.
* One DX token represents 1 Vote
* The maximum amount of candidates that a delegator can vote is 30.
* If the candidate became a validator, then delegators who voted for that validator will get reward.

### Step1.1 Get Candidate List

You have to check the candidate information before voting. To get detailed candidate information, you must know the candidate list first. Typing the following command in the console to retrieve candidate list:

```shell
> dpos.candidates()
```

### Step1.2 Check Candidate Information

Choose one candidate from the list above, then type the following command to retrieve its detailed information:

> NOTE: replace CANDIDATE_ADDRESS with one of the candidate addresses you retrieved from the previous step

```shell
> dpos.candidate("CANDIDATE_ADDRESS")
```

### Step1.3 Vote

To vote for the candidates you desired, type the following command in the console. By using the command below, you will vote for a list of candidates by depositing 2 DX token.

> NOTE: replace CANDIDATE_ADDRESSES with a list of candidates addresses you want to vote, seperate them by comma. The max amount of candidates you can vote is 30.

```shell
> dpos.vote({from:eth.accounts[0], candidates:"CANDIDATE_ADDRESSES",deposit:"2dx"})
```

### Step1.4 Cancel Vote

To get back your vote deposit, you must send the cancel vote transaction. Typing the following command in the console

```shell
> dpos.vote(eth.accounts[0])
```

## Section Two: Candidate Tutorial

**Candidate Introduction:**
* Candidate gets votes from delegator and compete with each other to become a validator. 
* Validators are same as miners, which can get reward by validating transactions and producing blocks.
* Anyone who deposits 10000 DX token can become a candidate.
* Candidate must specify the reward distribution rules, so when he became a validator, the block reward will be distributed among delegators and the candidate.

### Step2.1. Apply for Candidate

To apply for the candidate, you must specify the deposit you are willing to put and the ratio for distributing the reward. By typing the following command, you will deposit 10000 DX token, and for each block reward you received, 50% of it will be distributed among delegators who voted for you and yourself.

```shell
> dpos.applyCandidate({ratio:"50",deposit:"10000dx"})
```

### Step2.2. Start Mining

Once you applied for candidate, start the mining directly by typing the following command:

> Note: you will not be able to mine any block unless you became a validator. It is just safe for you to start mining earlier because at the time you became a validator, mining operation will be performed automatically so you will not miss any block.

```shell
> miner.start()
```

### Step2.3. Check Candidate List

Wait about 10 seconds for candidate apply transaction to be processed, then type the following command in the console to check if you are in the candidate list.

```shell
> dpos.candidates()
```

### Step2.4. Candidate Cancellation

To get back your candidate deposit, you must quit on being a candidate. Type the following command in the console to send transaction for cancelling candidate:

> NOTE: your deposit will be returned in two days

```shell
> dpos.cancelCandidate(eth.accounts[0])
```
