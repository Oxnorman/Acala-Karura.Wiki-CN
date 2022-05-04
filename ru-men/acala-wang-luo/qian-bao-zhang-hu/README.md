# 钱包 & 账户

本文档主要是Acala, Karura, Polkadot 和 Kusama 账户地址的一些基本介绍

## 地址格式 <a href="#address-format" id="address-format"></a>

Acala和Karura使用基于Substrate的SS58链地址格式。 更多消息请点击 [这里](https://wiki.polkadot.network/docs/en/learn-accounts).

* Acala 地址一般是以2开头，但也不一定总是这样
* Karura 地址一般以小写字母开头，比如  l, r, p, q, o...
* Polkadot 地址总是以数字1开头
* Kusama 总是以大写字母开头比如 C, D, F, G, H, J...
* Substrate 通用地址以5开头

## 存在性存款 <a href="#existential-deposit" id="existential-deposit"></a>

Acala使用 [_存在性存款_ (ED)](https://wiki.polkadot.network/docs/learn-accounts#existential-deposit-and-reaping) 来避免太多睡眠账户使得存储的状态数据太过沉重。如果一个账户的存款少于ED, 那么该账户的状态将会从区块链中抹去以保护稀有的链上存储资源。随即该账户余额会被删除并且捐入国库。你仍然可以进入到账户中，但是账户已经没有了链上状态。&#x20;

转账：当你从账户A转移一定数量token到账户B

* 如果在转账完成后，A账户的余额低于ED，它将会被移除。所以请确保有足够的的余额来保证A账户的活跃状态
* 如果B账户没有余额并且转账金额少于ED，账户B就会想从没收到这笔资金一样，因为他的状态会从链上删除。所以也要保证发出足够的金额来使新账户活跃

**兑换**: 当你用Token A兑换Token B，如果token A的账户余额小于ED要求，该交易可能失败。任何人都可以用acala.js SDK来构建一个前端，帮助自己促进交易和检查ED，请谨记这一点。

**领取奖励**: 当领取LP token或者其他奖励时，如果在领取奖励之后，余额依然少于ED的要求，该账户的余额可能会被清除。ED要求适用于所有token账户，每一种token账户都有自己的ED要求。比如说，DOT账户的余额少于ED，你的DOT余额将会被移除，但其他资产的余额并不会受到影响。任何改变某一特定token余额的交易，如兑换等，都会引起ED的判定，所以你要时常留意ED要求。下面是在Karura网络上token的ED要求

* ACA ED: 0.1 ACA
* aUSD ED: 0.1 aUSD
* DOT ED: 0.01 DOT
* LDOT ED: 0.05 LDOT

你可以通过查询链上常数`balances.existentialDeposit`([ED Runtime Code](https://github.com/AcalaNetwork/Acala/blob/35078ea2b2d0e3a3937a075c54d94c77faea2f36/runtime/acala/src/lib.rs#L752-L754))([ED SDK](https://github.com/AcalaNetwork/acala.js/blob/master/packages/sdk-wallet/src/utils/get-existential-deposit-config.ts))来验证Aca的存在性存款

## 生成账户 <a href="#account-generation" id="account-generation"></a>

在网络上线前和初始化阶段，如下是生成Acala和Karura账户的推荐方法:

* Polkadot{.js} 浏览器插件

## Polkadot{.js} 浏览器插件 <a href="#polkadot-.js-browser-plugin" id="polkadot-.js-browser-plugin"></a>

### 安装浏览器插件 <a href="#install-the-browser-plugin" id="install-the-browser-plugin"></a>

在 [Google Chrome](https://chrome.google.com/webstore/detail/polkadot%7Bjs%7D-extension/mopnmbcafieddcagagdcbnhejhlodfdd?hl=en) (以及基于Chromium的浏览器如Brave) 和 [FireFo](https://addons.mozilla.org/en-US/firefox/addon/polkadot-js-extension) 上都可以安装浏览器插件。在 [这里](https://polkadot.js.org/extension/)下载插件.

![](https://1503523808-files.gitbook.io/\~/files/v0/b/gitbook-legacy-files/o/assets%2F-MAz4EenwXLth\_HO\_hmJ%2F-M\_d9J85pM55GhyGPGd1%2F-M\_dCLYCSww-lIL9hYYX%2FScreen%20Shot%202021-05-14%20at%204.49.27%20PM.png?alt=media\&token=1145ec94-8c95-4130-b530-f8db80523273)

### 创建账户 <a href="#create-account" id="create-account"></a>

点击你浏览器顶端Polkadot{.js} 的logo，就能打开浏览器插件了。你将看到一个浏览器弹窗，点击加号按钮然后在右上角的小图标中选择“创建新账户”。 Polkadot{.js} 插件将利用系统的随机性为你的账户生成种子然后以12个单词的形式展示给你。

![](https://1503523808-files.gitbook.io/\~/files/v0/b/gitbook-legacy-files/o/assets%2F-MAz4EenwXLth\_HO\_hmJ%2F-M\_d9J85pM55GhyGPGd1%2F-M\_dDK3C-NtFvAMNwiSt%2FScreen%20Shot%202021-05-14%20at%204.53.46%20PM.png?alt=media\&token=e19bcc1d-89fe-4403-a98b-1fd9dfc794b5)

你应当对这些单词进行备份，详细信息在[这里](https://wiki.polkadot.network/docs/en/learn-account-generation#storing-your-key-safely)。非常有必要将这些种子助记词存储在一个安全以及隐蔽的地方。如果你由于一些原因不能够通过Polkadot{.js} 来连接到你的账户，你可以通过“添加账户菜单”中的“通过种子助记词来导入账户”来重新添加已有账户。

![](https://1503523808-files.gitbook.io/\~/files/v0/b/gitbook-legacy-files/o/assets%2F-MAz4EenwXLth\_HO\_hmJ%2F-M\_d9J85pM55GhyGPGd1%2F-M\_dD50MlKV95MR4yG4t%2FScreen%20Shot%202021-05-14%20at%204.52.43%20PM.png?alt=media\&token=2b723190-b2bd-4cb3-99ec-d65d39ecb53a)

### 账户名称和密码 <a href="#name-account-and-password" id="name-account-and-password"></a>

你可以给你的账户随意取名，并且只为你自己使用。密码是用来加密账户信息的。当使用账户来进行任何交易或者使用它来加密签名信息时，你需要重新填写密码。请注意，该密码**无法**保护你的种子助记词。如果某人知道了你的12个单词的助记词。他们仍然可以控制你的账户，即使他们不知道你的密码。

![](https://1503523808-files.gitbook.io/\~/files/v0/b/gitbook-legacy-files/o/assets%2F-MAz4EenwXLth\_HO\_hmJ%2F-M\_d9J85pM55GhyGPGd1%2F-M\_dDr2uh8p2z6RRpQYf%2FScreen%20Shot%202021-05-14%20at%204.54.44%20PM.png?alt=media\&token=a52161e9-6901-4e6e-9c43-d8712b5fce93)

### 为Acala主网设置地址 <a href="#set-address-for-acala-mainnet" id="set-address-for-acala-mainnet"></a>

现在我们将确保地址按照Acala主网地址的方式进行展示。点击插件窗口右上角的“Option”按钮，在 "Display address format for" 中选择 "Acala".**你的地址格式就可见了**- 由于得出你地址的数据是复用的，**所以你可以在多个链上使用相同的地址**。你可以通过点击账户的图片来复制你的地址。

![](https://1503523808-files.gitbook.io/\~/files/v0/b/gitbook-legacy-files/o/assets%2F-MAz4EenwXLth\_HO\_hmJ%2F-M\_d9J85pM55GhyGPGd1%2F-M\_dEaN0F2NnxThLxNu-%2FScreen%20Shot%202021-05-14%20at%204.58.59%20PM.png?alt=media\&token=4839beea-10bf-472b-82af-6e30c0db77b7)

### 为Karura主网设置地址 <a href="#set-address-for-karura-mainnet" id="set-address-for-karura-mainnet"></a>

点击插件窗口右上角的Options" ， 在 "Display address format for" 中选择 "Karura".**你的地址格式就可见了** - 由于得出你地址的数据是复用的，**所以你可以在多个链上使用相同的地址**。你可以通过点击账户的图片来复制你的地址。

![](https://1503523808-files.gitbook.io/\~/files/v0/b/gitbook-legacy-files/o/assets%2F-MAz4EenwXLth\_HO\_hmJ%2F-MbdDEGgoJvrmdLhrFQe%2F-MbdRZuBQFh3CP9oYLi9%2FScreen%20Shot%202021-06-08%20at%202.27.20%20PM.png?alt=media\&token=1c6e7440-9615-412c-a1e0-dd01559acf0f)

### 为Polkadot主网设置地址 <a href="#set-address-for-polkadot-mainnet" id="set-address-for-polkadot-mainnet"></a>

点击插件窗口右上角的Options"，在 "Display address format for" 中选择 "Polkadot".**你的地址格式就可见了** - 由于得出你地址的数据是复用的，**所以你可以在多个链上使用相同的地址**。你可以通过点击账户的图片来复制你的地址。

![](https://1503523808-files.gitbook.io/\~/files/v0/b/gitbook-legacy-files/o/assets%2F-MAz4EenwXLth\_HO\_hmJ%2F-M\_lyAqaQ1Db6r48e1UC%2F-M\_lzxaAC\_H6sfIeMChL%2FScreen%20Shot%202021-05-16%20at%209.45.59%20AM.png?alt=media\&token=b17daac9-6d88-44e2-892a-4a797d5805b3)

### 为Kusama主网设置地址 <a href="#set-address-for-kusama-mainnet" id="set-address-for-kusama-mainnet"></a>

点击插件窗口右上角的Options" ， 在 "Display address format for" 中选择 "Kusama".**你的地址格式就可见了** - 由于得出你地址的数据是复用的，**所以你可以在多个链上使用相同的地址**。你可以通过点击账户的图片来复制你的地址。

![](https://1503523808-files.gitbook.io/\~/files/v0/b/gitbook-legacy-files/o/assets%2F-MAz4EenwXLth\_HO\_hmJ%2F-M\_lyAqaQ1Db6r48e1UC%2F-M\_m-313S-tBRN22FXN1%2FScreen%20Shot%202021-05-16%20at%209.46.09%20AM.png?alt=media\&token=ae33d5a2-1d7a-4fa3-8138-68055b992dfe)

### 将地址转换成不同链的格式 <a href="#convert-address-for-different-chain-formats" id="convert-address-for-different-chain-formats"></a>

你可以使用 [Subscan 地址转换工具 ](https://polkadot.subscan.io/tools/ss58\_transform) 在不同链的地址格式之间进行转换。在左手边的输入格内输入任意地址，然后点击 **`Transform`** 按钮，你就可以看到右手边出现了所有可能的地址格式。

## **Polkawallet** <a href="#polkawallet" id="polkawallet"></a>

### **安装 Polkawallet** <a href="#install-polkawallet-app" id="install-polkawallet-app"></a>

通过[官网](https://polkawallet.io)下载Polkawallet钱包. 对于iOS设备，可以通过Apple应用商店下载，安卓设备可通过 Google Play 下载，或者安卓APK。

### 创建账户 <a href="#create-account-1" id="create-account-1"></a>

1. 点击 "Create Account" 按钮.

2\. 一个新的界面会出现，主要提醒用户将助记词存到安全的地方。点击 "Next" 。

‌

![](https://lh6.googleusercontent.com/509\_xAUccOu0djt4YJZsvrLW4H\_fdBxmOmMMwpRrseGSt9xcyZdx4Tgge7ZofXk6um7rSR6LcPL7c23rJHF2ZHv7FlLl2SbYciqd3-ck\_v\_hlco0RRP7oPpin90nv2YETvvN\_cEb)

3\. 此时你的助记词将呈现。将助记词记录在纸上或者将其存在安全地方。然后点击  "Next" 。

![](https://lh5.googleusercontent.com/XD1NG32OkmzZYToN8Fb-noLzUJmacWIACYhi-gSyV3-s58n4Ovu6sS0qQMRe1NkMMyLA4LBz\_wEHRnEDwVnQgEaXQwCrgvUr0fNvA8SDilS7mrrnP--9bx3-SnHaioy\_prFD4KoE)

4\. 通过输入刚才助记词的内容和顺序来确定你已经记好助记词，然后在完成时点击 "Next" 。

![](https://lh4.googleusercontent.com/ROVs8A4woJy9RYKmsGd6Jm1W8GMzG\_cpB6ba3XLViS18GMTmRK0giSV7qkDh2XZrKxxLv4LFLEFuiRT6Lw3wri8yu6cT9tBMyw00vMhxq5Vmwb2qBOUg9-Eey7RHMbh4araqvk7P)

![](https://lh5.googleusercontent.com/VaB4EcpFPO9Qmvl2K\_MVKk8rVevhEzDsD45WZzkWKe3B6DXyoSU8-IenMk3slTe4uGLVl4IzAEmOz-A0SyJ508VUy49UfiGpsBT5R7q2QRmeybP1cE-2fU52iOdoudgcdmsLv\_Kl)

### **账户名和密码** <a href="#name-account-and-password-1" id="name-account-and-password-1"></a>

给你的账户命名，并且创建一个高强度的密码（至少6个字符），然后在完成后点击 "Next" 。

![](https://lh4.googleusercontent.com/PWXIJxAuCBlb-QGBrpce0gvFgG\_C\_jWUL125eOU\_ke\_thRY4WDhUq1AvDa6bAWHWy\_sD5BXp40gM5zzJRdkDGF5XrtLEuLD5TwJ1sV8FDdjr1QRjDm9I-hzfXGsqBLsq0QVFgb02)

现在你的钱包就已经设置好了！你的主界面会默认跳转到Polkadot网络。在账户名下面的灰色内容来确认当前你正连接到哪一个网络。在如下的截屏图片中，它写的是"Polkadot."

![](https://lh5.googleusercontent.com/xlFLRGhSFMpRc1QeJrObC8vazj7YCLIe2AvW-euSwN4bvjlZWhTbcyBxF4SPTXQGuOCJtdxMW\_1IMNyoL88RzC51RGN7CkLepjjOXTnJkEkp0ZSRzS58F7rAVMamcuXJ\_01S6AhE)



### 为Polkadot主网设置地址 <a href="#set-address-for-polkadot-mainnet-1" id="set-address-for-polkadot-mainnet-1"></a>

1. 点击右上角的菜单按钮

![](https://i.imgur.com/JwPrsVe.jpg%20=250x)

2\. 在打开的菜单栏里选择Polkadot 的logo，点击出现在主屏幕中的地址。

![](https://i.imgur.com/YGx8nne.jpg%20=250x)

### 为Kusama主网设置地址 <a href="#set-address-for-kusama-mainnet-1" id="set-address-for-kusama-mainnet-1"></a>

1. 点击右上角的菜单按钮.
2. 在打开的菜单栏中选择Kusama的logo，然后点击出现在主屏幕上的地址

### Set Address for Acala Mainnet  <a href="#set-address-for-acala-mainnet-coming-soon" id="set-address-for-acala-mainnet-coming-soon"></a>

### Set Address for Karura Mainnet  <a href="#set-address-for-karura-mainnet-coming-soon" id="set-address-for-karura-mainnet-coming-soon"></a>

​

### &#x20;<a href="#undefined" id="undefined"></a>

\
