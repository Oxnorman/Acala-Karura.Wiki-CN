# 连接到节点

使用Acala EVM你需要连接到Acala的一个节点。你有如下两种选择

1. 连接到已部署的测试网（由Acala维护）
2. 运行本地的Acala测试节点

## **1. 连接到已部署的测试网**

在[这里](https://wiki.acala.network/learn/get-started/public-nodes#mandala-test-network-nodes)查询所有可用的测试网节点。你可以使用 [Polkadot 浏览器](broken-reference) 来与节点通信，并且使用[EVM游乐场](../evm-you-le-chang.md)来部署和执行合约。

## **2. 运行一个本地Acala测试网节点**

或者，你可以运行一个本地Acala测试网节点。为了运行你自己的节点，你需要在你设备上安装[Docker](https://www.docker.com) 。如果你还没有安装，请参照[这里](https://docs.docker.com/get-docker/)的说明。

为了验证是否Docker已经成功安装，请运行如下指令T：

```bash
docker version
```

如果你接收到了版本号，你可以通过如下指令来开启你的本地Acala节点：

```bash
docker pull acala/acala-node:latest
docker run -it -p 9944:9944 -p 9933:9933 acala/acala-node:latest --dev --ws-external --rpc-external --rpc-cors=all
```

你节点的输出大致如下:

![](<../../../../../.gitbook/assets/1 (42).png>)
