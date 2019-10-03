# Go DxChain Tutorial

`gdx` program is built on top of the DxChain protocol. DxChain is a blockchain based P2P network for data storage. The core feature is that users can upload data to the network as a storage client or provide a data storage service for other peers in the network as a storage host. In addition, DxChain also contains features that are supported by other blockchains, such as distributed ledger and smart contracts.

This document introduces operations that each node is able to perform. Before trying out some new features, please make sure that you read and follow the steps carefully in [Section One: Preparation](#Section-One-Preparation).


* For DPOS tutorial, please click [here](#section-two-storage-tutorial)
* For storage tutorial, please click [here](#section-four-program-clean-start)

**Table of Contents:**

- [Go DxChain Tutorial](#go-dxchain-tutorial)
  - [Section One: Preparation](#section-one-preparation)
    - [Step1.1. Get the `gdx` Executable](#step11-get-the-gdx-executable)
    - [Step1.2. Executable Relocation](#step12-executable-relocation)
    - [Step1.3. Executable Verification](#step13-executable-verification)
    - [Step1.4. Grant Execute Permission](#step14-grant-execute-permission)
    - [Step1.5. Start Node](#step15-start-node)
    - [Step1.6. Open `gdx` Console](#step16-open-gdx-console)
    - [Step1.7. Create account](#step17-create-account)
    - [Step1.8. Get Test DX Token](#step18-get-test-dx-token)
    - [Step1.9. Unlock the account](#step19-unlock-the-account)
- [Section Two: Storage Tutorial](#section-two-storage-tutorial)
- [Section Three: DPOS Tutorial](#section-three-dpos-tutorial)
- [Section Four: Program Clean Start](#section-four-program-clean-start)
- [Contact Information](#contact-information)

## Section One: Preparation

### Step1.1. Get the `gdx` Executable

Use the link below to download the `gdx` executable that is suitable for your system, and rename it to `gdx`. Then, open the terminal.

**NOTE: the executable downloaded only supports 64bit operating system**

- Linux: [Download Link](download)
- MacOS: [Download Link](download)


### Step1.2. Executable Relocation

Create the `bin` folder under the home directory and place the `gdx` executable under it. To create the folder under the home directory, type the following command in the terminal.

```shell
$ mkdir ~/bin
```

### Step1.3. Executable Verification

For security purposes, when the executable is downloaded, you will need to verify that the program downloaded is the one we provided.

```shell
$ cd ~/bin
$ shasum -a 256 gdx
```

If the result you get from executing the commands above matches with one of the following hash values, it means the executable is the official one. Otherwise, delete the executable immediately and contact support@dxchain.com

- Linux: `064f8c190e1c594830b20c9794e025848477a019f3e5f4312ec1eefb3726b5b4 gdx`
- MacOS: `9162083f65b1f195574f4661515ffbaf5c1ae08045380e16692b99a67974d022 gdx`

### Step1.4. Grant Execute Permission

Without granting permission to execute, the system will not allow the `gdx` program to execute. To grant permission to execute, run the following command:

```shell
$ cd ~/bin
$ chmod +x gdx
```

### Step1.5. Start Node

**NOTE: if the node is running or previously ran, you must terminate the program by pressing `Ctrl + C` and then [clean start](#section-four-program-clean-start) the node.**

To start the node, simply type the following command in the terminal:

```shell
$ ~/bin/gdx
```

### Step1.6. Open `gdx` Console

Open another terminal panel and start the gdx console by using the following command:

```shell
$ ~/bin/gdx attach
```

### Step1.7. Create account

Once the gdx console is opened, type the following command to create an account:

```shell
> personal.newAccount("")
```

**NOTE: for simplification, the password used in this command is empty.**

### Step1.8. Get Test DX Token

After the account is created, you need to get some DX token in order to try out new features. Using the website [here](https://dxfaucet.dxchain.com) to get some test DX token.

### Step1.9. Unlock the account

If the account is locked, you will not be allowed to make any transaction. Typing the following command to unlock the account:

```shell
> personal.unlockAccount(eth.accounts[0], "", 0)
```

_Congratulations! You have completed Section One: Preparation!_

# Section Two: Storage Tutorial

> Note: it is important to finish the preparation steps before getting to storage tutorial

- [Storage Tutorial](storage_manual/storage_en.md)

# Section Three: DPOS Tutorial

> Note: it is important to finish the preparation steps before getting to DPOS tutorial

- [DPOS Tutorial](dpos_manual/dpos_en.md)

# Section Four: Program Clean Start

To start the node as a new node, the previously saved data must be removed (NOTE: this means everything will be reset.)

- For macOS: `rm -r ~/Library/DxChain`
- For linux: `rm -r ~/.dxchain`

Once the old data is removed, the node can be restarted.

# Contact Information

Thank you so much for your support and confidence in this project. If you have any question, please do not hesitate to contact DX via support@dxchain.com
