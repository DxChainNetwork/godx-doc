# Go DxChain Tutorial

Official Golang implementation of DxChain Protocol.

`gdx` program is built on top of the DxChain protocol. DxChain is a blockchain based P2P network for data storage. The core feature is that user can upload data to the network as storage client or provide data storage service for other peers in the network as a storage host. In addition, DxChain also contains features that are supported by other blockchains, such as distributed ledger and smart contracts.

This document introduces roles and functions that each node is able to become or perform. Before trying out some new features, please make sure that you read and follow the steps carefully in [Section One: Preparation](#Section-One-Preparation).

If you intend to become a miner, please click [here](#Section-Two-Miner).  
If you intend to become a storage client, please click [here](#Section-Three-Storage-Client).  
if you intend to become a storage host, please click [here](#Section-Four-Storage-Host).

**Table of Contents:**

- [Go DxChain Tutorial](#go-dxchain-tutorial)
  - [Important](#important)
  - [Section One: Preparation](#section-one-preparation)
    - [Step1.1. Get the `gdx` Executable](#step11-get-the-gdx-executable)
    - [Step1.2. Executable Relocation](#step12-executable-relocation)
    - [Step1.3. Executable Verification](#step13-executable-verification)
    - [Step1.4. Grant Execute Permission](#step14-grant-execute-permission)
    - [Step1.5. Version Verification](#step15-version-verification)
- [Section Two: Miner](#section-two-miner)
    - [Step2.1. Start Node](#step21-start-node)
    - [Step2.2. Open `gdx` Console](#step22-open-gdx-console)
    - [Step2.3. Create Account and Start Mining](#step23-create-account-and-start-mining)
    - [Step2.4. Stop Mining](#step24-stop-mining)
- [Section Three: Storage Client](#section-three-storage-client)
  - [Storage Client Execution Steps](#storage-client-execution-steps)
    - [Step3.1. Node Termination](#step31-node-termination)
    - [Step3.2. Start Node](#step32-start-node)
    - [Step3.3. Open `gdx` Console](#step33-open-gdx-console)
    - [Step3.4. Create Account and Start Mining](#step34-create-account-and-start-mining)
    - [Step3.5. Unlock Account](#step35-unlock-account)
    - [Step3.6. Check Balance](#step36-check-balance)
    - [Step3.7. Client Configuration](#step37-client-configuration)
    - [Step3.8. File Upload](#step38-file-upload)
    - [Step3.9. Upload Progress](#step39-upload-progress)
    - [Step3.10. File Download](#step310-file-download)
    - [Step3.11. File Verification](#step311-file-verification)
- [Section Four: Storage Host](#section-four-storage-host)
  - [Storage Host Execution Steps](#storage-host-execution-steps)
    - [Step4.1. Node Termination](#step41-node-termination)
    - [Step4.2. Start Node](#step42-start-node)
    - [Step4.3. Open `gdx` Console](#step43-open-gdx-console)
    - [Step4.4. Create Account and Start Mining](#step44-create-account-and-start-mining)
    - [Step4.5. Unlock Account](#step45-unlock-account)
    - [Step4.6. Check Balance](#step46-check-balance)
    - [Step4.7. Add Folder](#step47-add-folder)
    - [Step4.8. Host Announcement](#step48-host-announcement)
- [Section Five: Program Clean Start](#section-five-program-clean-start)
- [Contact Information](#contact-information)

## Important

**Please read Section One: Preparation carefully**

## Section One: Preparation

### Step1.1. Get the `gdx` Executable

Use the [link here](https://forms.gle/ymb8XKUVKAo2fuTc9) to submit the DxChain Testnet3.0 Test Node Application. When we received and reviewed your application, a download link will be sent to your email address. Download the `gdx` executable using the link provided and rename it to `gdx`. Then open the terminal.

**NOTE: the executable downloaded only supports 64bit operating system**

### Step1.2. Executable Relocation

Create the `bin` folder under the home directory and place the `gdx` executable under it. To create the folder under the home directory, typing the following command in the terminal.

```shell
$ mkdir ~/bin
```

### Step1.3. Executable Verification

For security purpose, when the executable is downloaded, you will need to verify that if the program you downloaded is the one we provided.

```shell
$ cd ~/bin
$ shasum -a 256 gdx
```

If the result you got from executing the commands above matches with one of the following hash value, it means the executable is the official one. Otherwise, delete the executable immediately and request for another downloading link.

- Linux: `1662649608ab85e8eb950a4365b4f7d0ddb267e9f6272a16dd17a399ffb5a8c1 gdx`
- MacOS: `8ed07b2ee18eed56c07ea9522654bed0620e502c3f5934e48b86e747732ec7e7 gdx`

### Step1.4. Grant Execute Permission

Without granting the execute permission, the system will not allow the `gdx` program to be executed. To grant execute permission, run the following command

```shell
$ cd ~/bin
$ chmod +x gdx
```

### Step1.5. Version Verification

Check the executable version by running the following command in the terminal. The expected version will be `Version: 0.7.2-unstable`

```shell
$ ~/bin/gdx version
```
_Congratulations! You have completed Section One: Preparation!_

# Section Two: Miner

Every node can become a miner regardless of its role. If you do not intend to become neither a storage client nor a storage host, you can start the program by running the following command in the terminal.

```shell
$ gdx
```

**NOTE: Both storage client and storage host have full functionality of miner.**

### Step2.1. Start Node

To start the node as a miner, please type the following commands in the terminal

```shell
$ ~/bin/gdx
```

### Step2.2. Open `gdx` Console

Open another terminal panel and start the gdx console by using the following command

```shell
$ ~/bin/gdx attach
```

### Step2.3. Create Account and Start Mining

To acquire tokens, you will first need to create an account and start mining. Typing the following commands in the `gdx` console you just opened.

```js
> personal.newAccount("")
> miner.start()
```

**NOTE: for simplification, the password used in this command is empty.**


### Step2.4. Stop Mining

To stop mining, simply type the following commands in the `gdx` console.

```js
> miner.stop()
```

# Section Three: Storage Client

By paying DX tokens to storage hosts, storage client is able to rent storage space and store files in the DX network safely and securely. When needed, storage client can download those files from the network.

To start the node as a storage client, run the following command in the terminal

```shell
$ gdx --storageclient
```

**NOTE: a node can either become a storage client or a storage host. To switch between two roles, you must [clean start](#Section-Five-Program-Clean-Start) the node**

## Storage Client Execution Steps

### Step3.1. Node Termination

**Note: skip step 3.1 if you have not yet to run the `gdx` program**

If the node is running or had ran previously, you must terminate the program by pressing `Ctrl + C`, and then [clean start](#Section-Five-Program-Clean-Start) the node

### Step3.2. Start Node

To start the node as the storage client, type the following commands in the terminal

```shell
$ ~/bin/gdx --storageclient
```

### Step3.3. Open `gdx` Console

Open another terminal panel and start the gdx console by using the following command

```shell
$ ~/bin/gdx attach
```

### Step3.4. Create Account and Start Mining

In order to create contract and start to upload file, you must have some tokens first. To get tokens, you will first need to create an account and start mining. Typing the following commands in the `gdx` console you just opened.

```js
> personal.newAccount("")
> miner.start()
```

**NOTE: for simplification, the password used in this command is empty**

### Step3.5. Unlock Account

If the account is locked, you will not be allowed to make any transaction. Therefore, we need to unlock the account by typing the following command in the console.

```js
> personal.unlockAccount(eth.accounts[0], "", 0)
```

**NOTE: if your account if protected by the password, you can replace `""` from the command above with `"YOUR_PASSWORD"`**

### Step3.6. Check Balance

As mentioned above, to create contract and then to upload files, you must have enough tokens. You can use the following command in the console to check the account balance. Wait until the result is not 0, and then you can proceed to the next step

```js
> eth.getBalance(eth.accounts[0])
```

**NOTE: Before you proceed to _Step3.7. Client Configuration_, please make sure that you have connected to at least 3 hosts and check their version. You can run the following code to get hosts number and check version, the correct version should be _1.0.1_**
```shell
sclient.hosts
```

### Step3.7. Client Configuration

To create contracts with storage hosts, you must specify the client configurations. By typing the following command in the console, the default configuration will be used

```js
> sclient.setconfig({})
```

Wait until 3 contracts are created. You can check number of contracts created by using the following command:

```js
> sclient.contracts.length
```

If error shows up, it means you haven't create any contract yet. It may take a while since you need to sync.

### Step3.8. File Upload

By typing the following commands in the terminal, a file named `upload.file` with random data will be created under the home directory. The file size is 512KB.

```shell
$ cd ~
$ dd if=/dev/urandom of=upload.file count=512 bs=1024
```

Then, get the absolute path of the file by using the following command  

```shell
$ cd ~
$ ls "`pwd`/upload.file"
```

In the `gdx` console, use the following command to upload the file.  
**Note: replace `FILE_PATH` with the absolute path of the file**

```js
> sclient.upload("FILE_PATH", "download.file")
```

### Step3.9. Upload Progress

To check the upload progress, type the following command in the console:

```js
> sclient.files
```

Wait util the upload progress reaches 100%, then you can proceed to the next step.

### Step3.10. File Download

When the file is uploaded, you will be able to download it. To download the file to the home directory, you need to first get the absolute path of the home directory by typing the following command in the terminal

```shh
$ cd ~
$ pwd
```

Then, typing the following command in the `gdx` console (**NOTE: replace `FILE_PATH` with the absolute path of the home directory**)

```js
> sclient.download("download.file", "FILE_PATH/download.file")
```

The file will be downloaded to your home directory as `download.file`

### Step3.11. File Verification

Since the file uploaded is generated and filled in with random data. To check if the file downloaded is the file you actually uploaded, use the following commands

```shell
$ cd ~
$ shasum -a 256 upload.file
$ shasum -a 256 download.file
```

If the hash value you got for upload.file matches with the hash value you got from download.file. It means two files are exactly the same.

# Section Four: Storage Host

Storage host serves as storage service provider, gaining profit for storing data uploaded by the storage client.

To start the node as a storage host, run the following command in the terminal

```shell
$ gdx --storagehost
```

**NOTE: a node can either become a storage client or a storage host. To switch between two roles, you must [clean start](#Section-Five-Program-Clean-Start) the node**
## Storage Host Execution Steps

### Step4.1. Node Termination

**Note: skip step 3.1 if you have not yet to run the `gdx` program**

If the node is running or had ran previously, you must terminate the program by pressing `Ctrl + C`, and then [clean start](#Section-Five-Program-Clean-Start) the node

### Step4.2. Start Node

To start the node as the storage host, type the following commands in the terminal

```shell
$ ~/bin/gdx --storagehost
```

### Step4.3. Open `gdx` Console

Open another terminal panel and start the gdx console by using the following command

```shell
$ ~/bin/gdx attach
```

### Step4.4. Create Account and Start Mining

In order to create contract with clients, you must have some tokens first. To get tokens, you will first need to create an account and start mining. Typing the following commands in the `gdx` console you just opened.

```js
> personal.newAccount("")
> miner.start()
```

**NOTE: for simplification, the password used in this command is empty.**

### Step4.5. Unlock Account

If the account is locked, you will not be allowed to make any transaction. Therefore, we need to unlock the account by typing the following command in the console

```js
> personal.unlockAccount(eth.accounts[0], "", 0)
```

**NOTE: if your account if protected by the password, you can replace `""` from the command above with `"YOUR_PASSWORD"`**

### Step4.6. Check Balance

As mentioned above, to create contract, you must have some tokens. Using the following command in the console to check the balance. Wait until the result is not 0, and then you can proceed to the next step

```js
> eth.getBalance(eth.accounts[0])
```

### Step4.7. Add Folder

To be able to save the data uploaded by the storage client, you must allocate disk space first. In the `gdx` console, type the following command to allocate `1 GB` disk space under the home directory, `temp` folder (Note: the folder `temp/dxchain` will be created under the home directory along with some files)

```js
> shost.addFolder("~/temp/dxchain", "1gb")
```

### Step4.8. Host Announcement

Lastly, announcement must be made to let other nodes knew that your node is a storage host node. By using the console command below, storage client will identify you as a storage host. (NOTE: you need to pay gas fee for doing this operation)

```js
> shost.announce()
```

# Section Five: Program Clean Start

To start the node as a new node, the previous saved data must be removed (NOTE: this means everything will be started from the beginning)

- For macOS: `rm -r ~/Library/DxChain`
- For linux: `rm -r ~/.dxchain`

Once the old data got removed, the node can be started as either storage client or storage host

# Contact Information

Thank you so much for your support and your confidence in this project. If you have any question, please do not hesitated to contact DX via support@dxchain.com
