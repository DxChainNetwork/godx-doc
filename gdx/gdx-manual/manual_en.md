# Go DxChain Tutorial

`gdx` program is built on top of the DxChain protocol. DxChain is a blockchain based P2P network for data storage. The core feature is that user can upload data to the network as storage client or provide data storage service for other peers in the network as a storage host. In addition, DxChain also contains features that are supported by other blockchain, such as distributed ledger and smart contracts.

In the DxChain Network, a node will always be able to perform mining operation regardless of the role the node choose to be. There are three roles available and each node can choose to become all of them at the same time or one of them only:
* Storage Client
* Storage Host
* Miner

This document introduces operations that each node is able to perform. Before trying out some new features, please make sure that you read and follow the steps carefully in [Section One: Preparation](#Section-One-Preparation).


* For miner tutorial, please click [here](#section-two-miner-tutorial)
* For storage client tutorial, please click [here](#section-three-storage-client-tutorial)
* For storage host tutorial, please client [here](#section-four-storage-host-tutorial)

**Table of Contents:**

- [Go DxChain Tutorial](#go-dxchain-tutorial)
  - [Important](#important)
  - [Section One: Preparation](#section-one-preparation)
    - [Step1.1. Get the `gdx` Executable](#step11-get-the-gdx-executable)
    - [Step1.2. Executable Relocation](#step12-executable-relocation)
    - [Step1.3. Executable Verification](#step13-executable-verification)
    - [Step1.4. Grant Execute Permission](#step14-grant-execute-permission)
    - [Step1.5. Version Verification](#step15-version-verification)
    - [Step1.6. Start Node](#step16-start-node)
    - [Step1.7. Open `gdx` Console](#step17-open-gdx-console)
- [Section Two: Miner Tutorial](#section-two-miner-tutorial)
    - [Step2.1. Create Account and Start Mining](#step21-create-account-and-start-mining)
    - [Step2.2. Stop Mining](#step22-stop-mining)
- [Section Three: Storage Client Tutorial](#section-three-storage-client-tutorial)
  - [Storage Client Execution Steps](#storage-client-execution-steps)
    - [Step3.1. Create Account and Start Mining](#step31-create-account-and-start-mining)
    - [Step3.2. Unlock Account](#step32-unlock-account)
    - [Step3.3. Check Balance](#step33-check-balance)
    - [Step3.4. Client Configuration](#step34-client-configuration)
    - [Step3.5. File Upload](#step35-file-upload)
    - [Step3.6. Upload Progress](#step36-upload-progress)
    - [Step3.7. File Download](#step37-file-download)
    - [Step3.8. File Verification](#step38-file-verification)
- [Section Four: Storage Host Tutorial](#section-four-storage-host-tutorial)
  - [Storage Host Execution Steps](#storage-host-execution-steps)
    - [Step4.1. Create Account and Start Mining](#step41-create-account-and-start-mining)
    - [Step4.2. Unlock Account](#step42-unlock-account)
    - [Step4.3. Check Balance](#step43-check-balance)
    - [Step4.4. Add Folder](#step44-add-folder)
    - [Step4.5. Host Announcement](#step45-host-announcement)
- [Section Five: Program Clean Start](#section-five-program-clean-start)
- [Contact Information](#contact-information)

## Important

**Please read the Section One: Preparation carefully**

## Section One: Preparation

### Step1.1. Get the `gdx` Executable

Use the [link here](https://forms.gle/ymb8XKUVKAo2fuTc9) to submit the DxChain Testnet3.0 Test Node Application. When we received and reviewed your application, a download link will be sent to your email address. Download the executable using the link provided and rename it to `gdx`. Then open the terminal.

**NOTE: the executable downloaded only supports 64bit operating system**

### Step1.2. Executable Relocation

Create the `bin` folder under the home directory and place the `gdx` executable under it. To create the folder under the home directory, typing the following command in the terminal.

```shell
$ mkdir ~/bin
```

### Step1.3. Executable Verification

For security purpose, when the executable is downloaded, you will need to verify that if the program downloaded is the one we provided.

```shell
$ cd ~/bin
$ shasum -a 256 gdx
```

If the result you got from executing the commands above matches with one of the following hash value, it means the executable is the official one. Otherwise, delete the executable immediately and request for another downloading link.

- Linux: `4d099c7f9a29e63eadb4ea1d3a3a840c6bc3a593a1f813d9222548e8a5235e24 gdx`
- MacOS: `123a264505df262ad50dccee7da5d115983ae13df7f4e99b471a87673ba90538 gdx`

### Step1.4. Grant Execute Permission

Without granting the execute permission, the system will not allow the `gdx` program to be executed. To grant execute permission, run the following command

```shell
$ cd ~/bin
$ chmod +x gdx
```

### Step1.5. Version Verification

Check the executable version by running the following command in the terminal. The expected version will be `Version: 0.8.0-unstable`

```shell
$ ~/bin/gdx version
```

### Step1.6. Start Node

**NOTE: If the node is running or had ran previously, you must terminate the program by pressing `Ctrl + C` and then [clean start](#Section-Five-Program-Clean-Start) the node**

To start the program as miner, storage client, and storage host, simply typing the following command in the terminal:

```shell
$ ~/bin/gdx
```

**Role Selection:**

If you do not intend to become neither a storage client nor a storage host, you can start the program by running the following command in the terminal:

```shell
$ ~/bin/gdx --role miner
```

To start the node as the storage client only, run the following command in the terminal:

```shell
$ ~/bin/gdx --role storageclient
```

To start the node as the storage host only, use the following command:

```shell
$ ~/bin/gdx --role storagehost
```

### Step1.7. Open `gdx` Console

Open another terminal panel and start the gdx console by using the following command. 

```shell
$ ~/bin/gdx attach
```

_Congratulations! You have completed Section One: Preparation!_

# Section Two: Miner Tutorial

### Step2.1. Create Account and Start Mining

To acquire tokens, you will first need to create an account and start mining. Typing the following commands in the `gdx` console you just opened.

```js
> personal.newAccount("")
> miner.start()
```

**NOTE: for simplification, the password used in this command is empty.**

### Step2.2. Stop Mining

To stop mining, simply type the following commands in the `gdx` console.

```js
> miner.stop()
```

# Section Three: Storage Client Tutorial

By paying DX tokens to storage hosts, storage client is able to rent storage space and store files in the DX network safely and securely. When needed, storage client can download those files from the network.

## Storage Client Execution Steps

**NOTE: skip the first two steps if the node is mining and the account is unlocked**

### Step3.1. Create Account and Start Mining

In order to create contract and start to upload file, you must have some tokens first. To get tokens, you will first need to create an account and start mining. Typing the following commands in the `gdx` console you just opened.

```js
> personal.newAccount("")
> miner.start()
```

**NOTE: for simplification, the password used in this command is empty**

### Step3.2. Unlock Account

If the account is locked, you will not be allowed to make any transaction. Therefore, we need to unlock the account by typing the following command in the console.

```js
> personal.unlockAccount(eth.accounts[0], "", 0)
```

### Step3.3. Check Balance

As mentioned above, to create contract and then to upload files, you must have enough tokens. You can use the following command in the console to check the account balance. Wait until the result is not 0, and then you can proceed to the next step

```js
> eth.getBalance(eth.accounts[0])
```

**NOTE: Before you proceed to _Step3.4. Client Configuration_, please make sure that you have connected to at least 3 hosts. You can run the following code to get the number of storage hosts. If error returned, it means no host is available yet**
```shell
sclient.host.ls.length
```

### Step3.4. Client Configuration

To create contracts with storage hosts, you must specify the client configurations. By typing the following command in the console, the default configuration will be used

```js
> sclient.setConfig({})
```

Wait until 3 contracts are created. You can check the number of contracts created by using the following command:

```js
> sclient.contracts.length
```

If error shows up, it means you haven't create any contract yet. It may take a while since you need to sync with the whole network.

### Step3.5. File Upload

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

### Step3.6. Upload Progress

To check the upload progress, type the following command in the console:

```js
> sclient.file.ls
```

Wait util the upload progress reaches 100%, then you can proceed to the next step.

### Step3.7. File Download

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

### Step3.8. File Verification

Since the file uploaded is generated and filled in with random data. To check if the file downloaded is the file you actually uploaded, use the following commands

```shell
$ cd ~
$ shasum -a 256 upload.file
$ shasum -a 256 download.file
```

If the hash value you got for upload.file matches with the hash value you got from download.file. It means two files are exactly the same.

# Section Four: Storage Host Tutorial

Storage host serves as storage service provider, gaining profit for storing data uploaded by the storage client.

## Storage Host Execution Steps

**NOTE: skip the first two steps if the node is mining and the account is unlocked**

### Step4.1. Create Account and Start Mining

In order to create contract with clients, you must have some tokens first. To get tokens, you will first need to create an account and start mining. Typing the following commands in the `gdx` console you just opened.

```js
> personal.newAccount("")
> miner.start()
```

**NOTE: for simplification, the password used in this command is empty.**

### Step4.2. Unlock Account

If the account is locked, you will not be able to make any transaction. Therefore, we need to unlock the account by typing the following command in the console

```js
> personal.unlockAccount(eth.accounts[0], "", 0)
```

### Step4.3. Check Balance

As mentioned above, to create contract, you must have some tokens. Using the following command in the console to check the balance. Wait until the result is not 0, and then you can proceed to the next step

```js
> eth.getBalance(eth.accounts[0])
```

### Step4.4. Add Folder

To be able to save the data uploaded by the storage client, you must allocate disk space first. In the `gdx` console, type the following command to allocate `1 GB` disk space under the home directory, `temp` folder (Note: the folder `temp/dxchain` will be created under the home directory along with some files)

```js
> shost.folder.add("~/temp/dxchain", "1gb")
```

### Step4.5. Host Announcement

Lastly, announcement must be made to let other nodes knew that your node is a storage host. By using the console command below, storage client will identify you as a storage host. (NOTE: you need to pay gas fee for doing this operation)

```js
> shost.announce()
```

# Section Five: Program Clean Start

To start the node as a new node, the previously saved data must be removed (NOTE: this means everything will be started from the beginning)

- For macOS: `rm -r ~/Library/DxChain`
- For linux: `rm -r ~/.dxchain`

Once the old data got removed, the node can be restarted.

# Contact Information

Thank you so much for your support and your confidence in this project. If you have any question, please do not hesitated to contact DX via support@dxchain.com
