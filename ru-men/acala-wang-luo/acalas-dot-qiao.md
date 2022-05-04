# Acala's DOT 桥

### Background <a href="#background" id="background"></a>

作为Polkadot生态的Defi中枢，Acala正建设围绕DOT的金融基础设施和生态系统。考虑到对于Polkadot的技术依赖，Acala正在采用一种分阶段的启动方法。其中一种依赖就是对于XCM桥这类基础设施的依赖，XCM桥是Polkadot生态的一部分用以实现在平行链之间的跨共识的通信。随着XCM的开发接近尾声， 预计它可能需要一段时间来进行测试和部署到更广范围内的生态系统中，但时间长度无法确定。为了满足社区对Acala上DOT流动性的渴望，我们很高兴地宣布一个临时的，非托管桥的解决方案，用以支持DOT转移到Acala，该方案已经得到Parity团队的支持。 尽管这只是一个有限的单向DOT桥，可以让DOT从Polkadot转移到Acala上，一旦XCM在Polkadot上可用，它就可以让DOT持有人无需迁移，就可无缝升级具有XCM能力。注意，关于从Acala上提取DOT，请参考如下文章：[交易所的存入和提取](qian-bao-zhang-hu/jiao-yi-suo-de-cun-qu-token.md)

### 什么是Acala的DOT桥 <a href="#what-is-the-acalas-dot-bridge" id="what-is-the-acalas-dot-bridge"></a>

Acala的DOT桥是针对如下问题给出的解决方案：

* 是一个非托管的DOT桥，从Polkadot到Acalai
* 为DOT持有者参与Acala的defi 经济提供了一条路径
* 当XCM可用时，就能够无缝升级新版本。对于DOT持有人来说不需要迁移或者额外的动作。

### 在你行动之前 <a href="#before-you-start" id="before-you-start"></a>

你应当意识到使用Acala桥的一些局限性：

* 将DOT从Polkadot带入到Acala是单向的，当前没有办法将该过程可逆-直到之前讨论到的XCM功能在Polkadot上面可用才行，或者从Acala上直接将DOT存入和取出到交易所功能实现才行。
* 只对 DOT有效，其他token或者资产无效
* 转移DOT数量超过5,000需要批准，这样可以作为一种额外的安全手段。该批准最多需要24小时来处理

### 如何使用桥? <a href="#how-to-use-the-bridge" id="how-to-use-the-bridge"></a>

如果你阅读了以上内容，仍然希望进行操作，那么我们欢迎你加入Acala世界！你可以看到一个手把手的指导[这里](https://app.gitbook.com/s/sAdRW4XXYoMPkA01Ntcp/kai-shi-shi-yong-acala/zhuan-zhang/zhuan-zhang-dot-dao-acala).​
