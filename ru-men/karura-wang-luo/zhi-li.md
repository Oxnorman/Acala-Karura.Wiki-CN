# 治理

阅读治理概况[这里](../../le-jie-acala/zhi-li-gai-shu/).如下是治理的讨论以及提案的汇聚点：

* ​[Karura Subsquare - 讨论 & 查阅相关链上提案​](https://karura.subsquare.io)
* ​[Polkadot Web App - 链上投票](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Facala-rpc-0.aca-api.network#/extrinsics)​
* ​[Acala 讨论论坛 - 内容详尽，非正式讨论](https://acala.discourse.group/c/acala/16)​

## 治理参数 <a href="#governance-parameters" id="governance-parameters"></a>

这些是重要的治理参数，可能会随着治理进程的前进而改变。

* 启动窗口期：公投**每2天**启动一次
* 投票窗口期：投票**每2天**统计一次
* 紧急投票窗口：快速通道的紧急公投窗口期是**3小时**
* 最少存款：提议一个公投提案所需的最小存款为**100KAR**
* 颁布期：锁定资金的最短期限和提案被批准到颁布之间的时间为1**天**
* 冷却期：被否决的提案在**7天内**不得重新提交

大多数这些参数都可以在Polkadot app上找到。你也可以在`Event Calendar`查阅未来的治理事件。

![](<../../.gitbook/assets/1 (67).png>)

## 提议公投提案 <a href="#propose-a-referendum" id="propose-a-referendum"></a>

一个全民公投由多个提议的草案构成。如果被Token持有人投票通过，该草案将会在链上自动颁布。你需要绑定一定数量的token来提议一个草案。一旦提议被提交，就不能取消了.&#x20;

在 [Polkadot Apps - Karura parachain](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fkarura-rpc-1.aca-api.network#/democracy), 你可以使用“民主”按钮来构建一个新的提案。草案，比如“强制将A账户的余额转移到B账户”，编码成为preimage，该草案的哈希值被称为preimage的哈希值。

由于preimage可能会很大（因此递交的成本很高），你可以先递交一个提案，该提案里面只包含preimage哈希值（或者让其他人为你递交），然后在投票完成前递交preimage。

### 步骤 1: 递交提案

#### 获取preimage哈希值

通过点击 `Submit preimage` 按钮, 你就可以填写你想提出的草案，复制并记下preimage的哈希值。`0x244fcb51680c90172ba55241d3d9229676c4471a4645aed223a2272b33264026`. 一旦你记下哈希值，你就可以取消提示了。

![](<../../.gitbook/assets/1 (24).png>)

#### 递交提案

通过点击 `Submit a proposal` 按钮来递交提案，并且将preimage的哈希值粘贴上去来完成递交。然后你就可以看到提案出现在提案栏里了。&#x20;

![](<../../.gitbook/assets/1 (20).png>)

### 步骤 2: 递交 Preimage

在开始对你提案进行公投钱，你需要递交你真实的preimage。不然提案不会在链上颁布。你可以重复上面“递交提案”的过程，然后点击“递交preimage”按钮来发送交易。

## 对公投提案投票

你必须持有KAR token并且这些token必须放在具有参与民主治理功能的钱包（比如Polkadot.js）里时，你才能在公投中投票。如果你在Polkadot.js的钱包里没有token，你可以在[这里](https://wiki.acala.network/karura/get-started/karura-account)阅读关于账户生成的信息。

一旦提案进入公投程序，他就会显示在公投表中。你可以导航到 [Polkadot Apps - Karura Parachain Democracy](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fkarura-rpc-1.aca-api.network#/democracy) 来投票.

![](<../../.gitbook/assets/1 (27).png>)

你可以点击 ‘Vote’ 按钮来投票. 选择 "Vote Aye" 来支持提案, 以及选择 "Vote Nay" 来反对一个提案。

你也可以通过锁定相同数量的token来表现你对一个提案的信心。你锁定token的时间越长，你投票的权重就会越高。阅读更多关于[投票](https://wiki.polkadot.network/docs/maintain-guides-democracy/#voting-on-a-proposal)和[计票](https://wiki.polkadot.network/docs/learn-governance#tallying)的信息.

![](<../../.gitbook/assets/1 (2).png>)

## 解锁锁定的token <a href="#unlock-locked-tokens" id="unlock-locked-tokens"></a>

一旦锁定期结束，你就需要解锁这些token。你要前往 `Accounts` 页面, 点击投票账户的菜单栏按钮，选择菜单项 `Clear expired democracy locks` 来取回Token. 阅读更多信息点击 [这里](https://wiki.polkadot.network/docs/maintain-guides-democracy/#unlocking-locked-tokens)。

![](<../../.gitbook/assets/1 (1).png>)

### 检查锁定的民主投票

前往 `Developer` - `Chain state` ，然后选择 `democracy` 和 `locks`. 在下拉菜单中选择用户投票的账户，然后点击 `+` 按钮来查询是否有锁定的投票以及如果有的话，他们需要被锁定多久。

![](<../../.gitbook/assets/1 (62).png>)

## 代表投票&#x20;

你可以指定其他人代替你进行投票。在 [the Polkadot Apps - Karura parachain](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fkarura-rpc-1.aca-api.network#/extrinsics), 前往 `Developer`  -- `Extrinsics` , 然后选择 `democracy.delegate` 。

![](<../../.gitbook/assets/1 (72).png>)
