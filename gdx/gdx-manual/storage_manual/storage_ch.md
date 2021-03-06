# Go DxChain 存储教程

## 第一部分：存储委托方教程

存储委托方通过支付DX通证，从存储提供方租借空间，把自己的文件，安全的存到DX网络中，并在需要的时候，从DX网络中下载已经上传的文件。

### 步骤1.1 检查余额

您需要向存储提供方支付DX通证以获取服务。您可以通过在控制台中输入以下命令查看余额。
```js
> eth.getBalance(eth.accounts[0])
```
当您的余额不是0的时候，您可以继续接下来的操作。

> 注意：在您执行*步骤1.2 委托方设定*之前请确保您已经和至少三个存储提供方连接. 您可以通过在控制台输入以下命令查看存储提供方的数量。如果您在输入以下命令时控制台返回一个错误，不要担心，这说明还没有存储提供方还没有找寻到存储供应商。这可能需要一小会儿，请您稍作等待

```shell
sclient.host.ls.length
```

### 步骤1.2 存储委托方设置

在您和存储提供方建立合约之前，您必须先进行存储委托方的设置。不用担心，DX已经为您准备好了一套默认设定，您只需要在控制台中输入以下命令即可。
```js
> sclient.setConfig({})
```

接下来请您稍作等待，您的节点此时正在与存储提供方节点建立合约，你可以通过在控制台输入以下命令查看已经建立的合约数量，当合约数量为3的时候您可以进行下一步操作。
```js
> sclient.contracts.length
```
如果您在输入以上命令时控制台返回一个错误，不要担心，这说明还没有存储提供方与您建立合约。这可能需要一小会儿，请您稍作等待

### 步骤1.3 上传文件

在上传文件之前，请您先在终端中输入以下命令，在Home路径下创建一个名为 upload.file 的文件。文件大小为 512KB。
```shell
$ cd ~
$ dd if=/dev/urandom of=upload.file count=512 bs=1024
```
接下来，请取得您将要上传的文件的绝对路径，你可以在终端输入以下命令。
```shell
$ cd ~
$ ls "`pwd`/upload.file"
```

接下来，请您在控制台中输入以下命令。

**注意：请把 FILE_PATH 替换成您刚刚取得的文件绝对路径。**

```js
> sclient.upload("FILE_PATH", "download.file")
```


### 步骤1.4 上传进度

您可以通过在控制台输入以下命令来查看上传进度。
```js
> sclient.file.ls
```
当文件上传进度到达100%时，您可以继续下一步的操作。

### 步骤1.5 下载文件

当文件完成上传后，您就可以下载该文件。你需要在终端中输入以下命令来获取您的Home路径的绝对路径，以便于将文件下载到Home路径下。
```shell
$ cd ~
$ pwd
```

之后请在控制台中输入以下命令。

**注意：请把FILE_PATH 替换成您刚刚取得的文件绝对路径。**

```js
> sclient.download("download.file", "FILE_PATH/download.file")
```

请您稍等片刻，一个名为`download.file`的文件将会被下载到您的Home路径下。

### 步骤1.6 验证文件

因为您上传的文件是一个随机生成的文件，如果您想检查下载下来的文件是否与上传的文件是同一个文件，您可以通过查看两个文件的哈希值来确认。请在终端中输入以下命令。
```shell
$ cd ~
$ shasum -a 256 upload.file
$ shasum -a 256 download.file
```
如果`upload.file`的哈希值与`download.file`的哈希值一样，则代表两个文件为同一文件。

## 第二部分：存储提供方教程

存储提供方为存储服务的提供者。存储提供方可以通过为存储委托方提供存储空间盈利。

### 步骤2.1 检查余额

您需要向存储提供方支付DX通证以获取服务。您可以通过在控制台中输入以下命令查看余额。
```js
> eth.getBalance(eth.accounts[0])
```
当您的余额不是0的时候，您可以继续接下来的操作。

### 步骤2.2 添加文件夹

为了使存储委托方可以正常的使用存储服务，您必须先对您的硬盘空间进行分配。在控制台中请您输入以下命令。这行命令将会在您的Home路径下创建一个大小为1gb，文件名为`temp`的文件夹，在`temp`文件夹下将会出现一个`dxchain`文件夹，里面包括了一些必要的文件。
```js
> shost.folder.add("~/temp/dxchain", "1gb")
```

### 步骤2.3 存储提供方声明

最后，您必须进行声明以供其他节点知晓您是一个存储提供方节点。通过在控制台中输入以下命令，存储委托方将知晓您是存储提供方。
```js
> shost.announce()
```