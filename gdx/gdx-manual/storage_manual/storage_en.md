
# Go DxChain Storage Tutorial

- [Go DxChain Storage Tutorial](#go-dxchain-storage-tutorial)
  - [Section One: Storage Client Tutorial](#section-one-storage-client-tutorial)
    - [Step1.1. Check Balance](#step11-check-balance)
    - [Step1.2. Client Configuration](#step12-client-configuration)
    - [Step1.3. File Upload](#step13-file-upload)
    - [Step1.4 Upload Progress](#step14-upload-progress)
    - [Step1.5. File Download](#step15-file-download)
    - [Step1.6. File Verification](#step16-file-verification)
  - [Section Two: Storage Host Tutorial](#section-two-storage-host-tutorial)
    - [Step2.1. Check Balance](#step21-check-balance)
    - [Step2.2. Add Folder](#step22-add-folder)
    - [Step2.3. Host Announcement](#step23-host-announcement)

## Section One: Storage Client Tutorial

By paying DX tokens to storage hosts, storage clients are able to rent storage space and store files in the DX network safely and securely. When needed, storage clients can download those files from the network.

### Step1.1. Check Balance

To create contracts and then upload files, you must have enough DX tokens. You can use the following command in the console to check the account balance. Wait until the result is not 0, and then you can proceed to the next step

```js
> eth.getBalance(eth.accounts[0])
```

> NOTE: before you proceed to _Step1.2. Client Configuration_, please make sure that you are connected to at least 3 hosts. You can run the following code to get the number of storage hosts you are connected to. If it returns an error, it means no host is available yet.
```shell
sclient.host.ls.length
```

### Step1.2. Client Configuration

To create contracts with storage hosts, you must specify the client configurations. By typing the following command in the console, the default configuration will be used

```js
> sclient.setConfig({})
```

Wait until 3 contracts are created. You can check the number of contracts created by using the following command:

```js
> sclient.contracts.length
```

If an error shows up, it means you haven't create any contract yet. It may take a while since you need to sync with the whole network.

### Step1.3. File Upload

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
>Note: replace `FILE_PATH` with the absolute path of the file. Keep the quotation mark.

```js
> sclient.upload("FILE_PATH", "download.file")
```

### Step1.4 Upload Progress

To check the upload progress, type the following command in the console:

```js
> sclient.file.ls
```

Wait until the upload progress reaches 100%, then you can proceed to the next step.

### Step1.5. File Download

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

### Step1.6. File Verification

The file uploaded is generated and filled with random data. To check if the file downloaded is the file you actually uploaded, use the following commands:

```shell
$ cd ~
$ shasum -a 256 upload.file
$ shasum -a 256 download.file
```

If the hash value you got for `upload.file` matches with the hash value you got from download.file. It means the two files are exactly the same.

## Section Two: Storage Host Tutorial

Storage hosts serve as storage service providers, gaining profit for storing data uploaded by the storage client.

### Step2.1. Check Balance

To create contracts, you must have some tokens. Use the following command in the console to check the balance. Wait until the result is not 0, and then you can proceed to the next step.

```js
> eth.getBalance(eth.accounts[0])
```

### Step2.2. Add Folder

To be able to save the data uploaded by the storage client, you must allocate disk space first. In the `gdx` console, type the following command to allocate `1 GB` of disk space under the home directory, `temp` folder (Note: the folder `temp/dxchain` will be created under the home directory along with some files)

```js
> shost.folder.add("~/temp/dxchain", "1gb")
```

### Step2.3. Host Announcement

Lastly, announcements must be made to let other nodes know that your node is a storage host. By using the console command below, storage client will identify you as a storage host. (NOTE: you need to pay gas fee for performing this operation.)

```js
> shost.announce()
```