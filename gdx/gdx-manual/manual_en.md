# Go DxChain Tutorial

`gdx` program is built on top of the DxChain protocol. DxChain is a blockchain based P2P network for data storage. The core feature is that users can upload data to the network as a storage client or provide a data storage service for other peers in the network as a storage host. In addition, DxChain also contains features that are supported by other blockchains, such as distributed ledger and smart contracts.

In the DxChain Network, a node will always be able to perform mining operation regardless of the role the node chooses to be. There are three roles available and each node can choose to become all of them at the same time or only one of them:
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

**Please read Section One: Preparation carefully**

## Section One: Preparation

### Step1.1. Get the `gdx` Executable

Use the [link here](https://forms.gle/ymb8XKUVKAo2fuTc9) to submit the DxChain Testnet3.0 Test Node Application. When we have received and reviewed your application, a download link will be sent to your email address. Download the executable using the link provided and rename it to `gdx`. Then, open the terminal.

**NOTE: the executable downloaded only supports 64bit operating system**

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

If the result you get from executing the commands above matches with one of the following hash values, it means the executable is the official one. Otherwise, delete the executable immediately and request for another download link.

- Linux: `dbe1c9eff6e28d9ee8b24ee29d83eae54ada630f0e3d012d39cc3fa743ea924a gdx`
- MacOS: `77fc8c4d110745ef132d61e408e174081926b49e6d47415bcc5c8979bd6b9b54 gdx`

### Step1.4. Grant Execute Permission

Without granting permission to execute, the system will not allow the `gdx` program to execute. To grant permission to execute, run the following command:

```shell
$ cd ~/bin
$ chmod +x gdx
```

### Step1.5. Version Verification

Check the executable version by running the following command in the terminal. The expected version will be `Version: 0.8.2-unstable`

```shell
$ ~/bin/gdx version
```

### Step1.6. Start Node

**NOTE: if the node is running or previously ran, you must terminate the program by pressing `Ctrl + C` and then [clean start](#Section-Five-Program-Clean-Start) the node.**

To start the program as a miner, storage client, and storage host, simply type the following command in the terminal:

```shell
$ ~/bin/gdx
```

**Role Selection (Optional):**

If you do not intend to become either a storage client or a storage host, you can start the program by running the following command in the terminal:

```shell
$ ~/bin/gdx --role miner
```

To start the node as a storage client only, run the following command in the terminal:

```shell
$ ~/bin/gdx --role storageclient
```

To start the node as a storage host only, run the following command in the terminal:

```shell
$ ~/bin/gdx --role storagehost
```

### Step1.7. Open `gdx` Console

Open another terminal panel and start the gdx console by using the following command:

```shell
$ ~/bin/gdx attach
```

_Congratulations! You have completed Section One: Preparation!_

# Section Two: Miner Tutorial

### Step2.1. Create Account and Start Mining

To acquire tokens, you will first need to create an account and start mining. Type the following commands in the `gdx` console you just opened:

```js
> personal.newAccount("")
> miner.start()
```

**NOTE: for simplification, the password used in this command is empty.**

### Step2.2. Stop Mining

To stop mining, simply type the following command in the `gdx` console:

```js
> miner.stop()
```

# Section Three: Storage Client Tutorial

By paying DX tokens to storage hosts, storage clients are able to rent storage space and store files in the DX network safely and securely. When needed, storage clients can download those files from the network.

## Storage Client Execution Steps

**NOTE: skip the first two steps if the node is mining and the account is unlocked**

### Step3.1. Create Account and Start Mining

In order to create contracts and upload files, you must have some tokens first. To get tokens, you will first need to create an account and start mining. Type the following commands in the `gdx` console you just opened:

```js
> personal.newAccount("")
> miner.start()
```

**NOTE: for simplification, the password used in this command is empty.**

### Step3.2. Unlock Account

If the account is locked, you will not be allowed to make any transactions. Therefore, we need to unlock the account by typing the following command in the console:

```js
> personal.unlockAccount(eth.accounts[0], "", 0)
```

### Step3.3. Check Balance

As mentioned above, to create contracts and then upload files, you must have enough tokens. You can use the following command in the console to check the account balance. Wait until the result is not 0, and then you can proceed to the next step

```js
> eth.getBalance(eth.accounts[0])
```

**NOTE: before you proceed to _Step3.4. Client Configuration_, please make sure that you are connected to at least 3 hosts. You can run the following code to get the number of storage hosts you are connected to. If it returns an error, it means no host is available yet.**
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

If an error shows up, it means you haven't create any contracts yet. It may take a while since you need to sync with the whole network.

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
**Note: replace `FILE_PATH` with the absolute path of the file. Keep the quotation mark**

```js
> sclient.upload("FILE_PATH", "download.file")
```

### Step3.6. Upload Progress

To check the upload progress, type the following command in the console:

```js
> sclient.file.ls
```

Wait until the upload progress reaches 100%, then you can proceed to the next step.

### Step3.7. File Download

When the file is uploaded, you will be able to download it. To download the file to the home directory, you need to first get the absolute path of the home directory by typing the following command in the terminal

```shh
$ cd ~
$ pwd
```

Then, type the following command in the `gdx` console (**NOTE: replace `FILE_PATH` with the absolute path of the home directory. Keep the quotation marks.**)

```js
> sclient.download("download.file", "FILE_PATH/download.file")
```

The file will be downloaded to your home directory as `download.file`

### Step3.8. File Verification

The file uploaded is generated and filled with random data. To check if the file downloaded is the file you actually uploaded, use the following commands:

```shell
$ cd ~
$ shasum -a 256 upload.file
$ shasum -a 256 download.file
```

If the hash value you got for upload.file matches with the hash value you got from download.file. It means the two files are exactly the same.

# Section Four: Storage Host Tutorial

Storage hosts serve as storage service providers, gaining profit for storing data uploaded by the storage client.

## Storage Host Execution Steps

**NOTE: skip the first two steps if the node is mining and the account is unlocked**

### Step4.1. Create Account and Start Mining

In order to create contracts with clients, you must have some tokens first. To get tokens, you will first need to create an account and start mining. Type the following commands in the `gdx` console you just opened.

```js
> personal.newAccount("")
> miner.start()
```

**NOTE: for simplification, the password used in this command is empty.**

### Step4.2. Unlock Account

If the account is locked, you will not be able to make any transactions. Therefore, we need to unlock the account by typing the following command in the console

```js
> personal.unlockAccount(eth.accounts[0], "", 0)
```

### Step4.3. Check Balance

As mentioned above, to create contracts, you must have some tokens. Use the following command in the console to check the balance. Wait until the result is not 0, and then you can proceed to the next step.

```js
> eth.getBalance(eth.accounts[0])
```

### Step4.4. Add Folder

To be able to save the data uploaded by the storage client, you must allocate disk space first. In the `gdx` console, type the following command to allocate `1 GB` of disk space under the home directory, `temp` folder (Note: the folder `temp/dxchain` will be created under the home directory along with some files)

```js
> shost.folder.add("~/temp/dxchain", "1gb")
```

### Step4.5. Host Announcement

Lastly, announcements must be made to let other nodes know that your node is a storage host. By using the console command below, storage client will identify you as a storage host. (NOTE: you need to pay gas fee for performing this operation.)

```js
> shost.announce()
```

# Section Five: Program Clean Start

To start the node as a new node, the previously saved data must be removed (NOTE: this means everything will be reset.)

- For macOS: `rm -r ~/Library/DxChain`
- For linux: `rm -r ~/.dxchain`

Once the old data is removed, the node can be restarted.

# Contact Information

Thank you so much for your support and confidence in this project. If you have any questions, please do not hesitate to contact DX via support@dxchain.com
