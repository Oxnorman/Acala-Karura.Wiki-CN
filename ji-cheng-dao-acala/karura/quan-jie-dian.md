# 全节点

## Spec 要求

与Kusama全节点要求一致

## 运行源代码

* 克隆 repo: [https://github.com/AcalaNetwork/Acala](https://github.com/AcalaNetwork/Acala)
* 在这里检查tag: [https://github.com/AcalaNetwork/Acala/tags](https://github.com/AcalaNetwork/Acala/tags)
* 安装dependencies
* 建设Karura: `cargo build --release --features with-karura-runtime`
* 运行 `./target/release acala --chain=karura`

## 使用 Docker

* Image: `acala/karura-node:latest` or `acala/karura-node:[version number]`
* `docker run acala/karura-node:latest --chain=karura`

## 常见CLI

* CLI 与任何基于Substrate的链基本相同
* 由于有两个节点服务正在运行中， `--` 用于分开plit CLI.  `--` 之前的程序发送给平行链的全节点服务执行， `--` 之后的程序发送给中继链全节点服务
  * 比如， `--chain=parachain.json --ws-port=9944 -- --chain=relaychain.json --ws-port=9945` 意味着
    * 平行链服务正在使用 `parachain.json` 作为链的配置，以及 web socket RPC 端口是9944
    * 中继链服务正在使用 `relaychain.json` 作为链的配置并使用web socket RPC端口是 9945
* 建议明确制定两个服务端口，以避免混淆
  * 比如 `--listen-addr=/ip4/0.0.0.0/tcp/30333 --listen-addr=/ip4/0.0.0.0/tcp/30334/ws -- --listen-addr=/ip4/0.0.0.0/tcp/30335 --listen-addr=/ip4/0.0.0.0/tcp/30336/ws`
* 建议为平行链添加 `--execution=wasm` 来避免同步问题

## CLI示例

### 归档 PRC Node

```
--base-path=/acala/data
--chain=karura
--name=rpc-1
--pruning=archive
--ws-external
--rpc-external
--rpc-cors=all
--ws-port=9944
--rpc-port=9933
--ws-max-connections=2000
--execution=wasm
--
--chain=kusama
```
