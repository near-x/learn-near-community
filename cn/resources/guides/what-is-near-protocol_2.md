# NEAR入门
## 账户/钱包
NEAR入门的第一件事，就是建立一个NEAR账户。

[请观看NEAR账户相关视频](https://youtu.be/2_Ekz7w6Eo4)


通过钱包，你可与发起智能合约调用，设置你的本地节点，收发资金。注册钱包账户ID时，你必须提供一个独一无二的名称。每个钱包都必须有唯一的名称，每个用户都可以创建多个钱包。

你可以想象这就类似脸书或者谷歌账户。一旦你注册了任一个服务，就可以使用相同的账户登录第三方服务。NEAR账户和谷歌账户之间的区别是那些代表账户的数据，是只能被钱包的所有者访问和管理的。除此以外，所有信息被存储在由节点组成的分布式网络上，而不是某个单独的服务器。

立刻[创建NEAR账户](https://wallet.near.org/create)

更多有关NEAR账户的内容请见[DOCS.NEAR](https://learnnear.club/doc/videos/accounts-keys/)

## NEAR 浏览器
NEAR 浏览器让你可以实时查看区块的创建！这个有用的工具可以查询[交易](https://learnnear.club/docs/concepts/transaction) 和 [账户](https://learnnear.club/docs/concepts/account)，让你可以查看用户和智能合约之间的所有交互。


# 如何获得NEAR通证?
有4种方式获得 $NEAR

## 以太坊用户可获得免费的NEAR
通过使用面向以太坊用户的水龙头[https://faucet.paras.id](https://faucet.paras.id)，用户可以得到一个拥有少量免费NEAR的钱包账户。

## 赚取NEAR
你可以通过参与[开发赏金任务](https://github.com/near/bounties)获得$NEAR, 运营一个帮助大家在NEAR上开发的[技术社区](https://near.org/guilds)，赢取NEAR骇客松比赛，或成为社区里的积极分子。如果你能吸引别人投NEAR给你抵押，你就可以成为一个验证人来赚取$NEAR。

## 购买NEAR
在一些大交易所（详情见下文）上都有$NEAR。在那里你可以注册并用加密货币或法币购买NEAR通证。

支持$NEAR的交易所

你可以在[coinmarketcap](https://coinmarketcap.com/currencies/near-protocol/) and [coingecko](https://www.coingecko.com/en/coins/near)上查看价格和交易对信息。

https://www.binance.com/en/my/wallet/exchange/deposit/crypto/NEAR

## 从朋友手里获得
你并不需要先有一个NEAR账户才能接收NEAR通证！“[NEAR Drop](https://near.org/blog/send-near-to-anyone-with-near-drops/)” 功能让你的朋友可以预付得到一个新账户并通过一个链接让你接收通证。

# 我拿着NEAR通证能做什么？
## 转账NEAR
将 $NEAR 在你和朋友的账户之间转来转去，并可以在[区块浏览器](https://explorer.mainnet.near.org/)里查看对应的交易。因为交易手续费非常低，你可以方便快捷的转移非常小额的NEAR玩玩。

把它们作为礼物通过[红包](http://redpacket.near.org/)送出去。

## 试试NEAR空投 (邀请朋友)
如果你的朋友向创建一个NEAR账户，可以给他们发送一个[NEAR空投](https://near.org/blog/send-near-to-anyone-with-near-drops/)。

## 使用NEAR应用
要查看日益增长的NEAR上的应用列表，[点击这里](https://awesomenear.com/categories/dapps/)。

轻松开启NFT之旅 - 购买/发布/交易 艺术品 就上 [https://paras.id/](https://paras.id/)

加入BerryClub参与艺术品的创作：[https://berryclub.io/](https://berryclub.io/)

# 使用NEAR的费用如何（Gas）？
当访问NEAR网络更新和改变数据时，运行网络基础架构的人就产生了一些开销。某些地方的某些计算机运行你的请求，而运营这些计算机的验证人需要支付显著的费用以确保这些计算机的运行。

与其他可编程网络类似，NEAR通过交易费，也叫Gas费补偿这些人。

如果你熟悉web2上的云服务提供商（亚马逊云，谷歌云等），区块链与其的最大不同是，用户在访问应用的时候直接支付费用，而不是开发者预付所有的基础设施费用。这带来了新的可能性，例如，应用本身规避了长期的入不敷出的资金风险。但这也带来了一些用户可用性上的问题。为了解决这个问题，NEAR也提供了让开发者支付用户使用开销的能力，让使用体验更靠近web2。

**考虑gas时要牢记的两个概念:**

1. Gas单位: 在内部，交易费不是直接用NEAR通证计算的，而是通过一个居中的gas单位。gas单位的好处是，他们是确定的，相同的交易总是消耗相同数量的gas单位。
2. Gas价格: gas单位乘以gas价格得到具体的向用户收取的费用。这个价格会在每个块时根据网络需求自动重新计算（如果前面块的gas数量超过半满，则价格上升，否则价格下降，每个块的价格变动不会超过1%）。最低的价格由网络配置决定，当前是1亿个yoctoNEAR。

注意：测试网和装的gas价格可能不同。在直接使用下面的数字之前，要检查一下gas价格。

**从gas角度看**

NEAR的出块时间在一秒左右，这归功于对每个区块gas数量的限制。Gas的单位经过仔细合理的计算，形成了一些易于理解的数字：

10¹² 个gas, 叫 1 TGas (TeraGas)…

≈ 1 毫秒的“计算”时间

…这样一来，在最小1亿个yoctoNEAR每gas的价格下，等值于0.1个milliNEAR。

这里的1ms是一个粗略但有用的近似值，也是目前NEAR中对gas单位设定的目标。Gas单位不仅封装了计算/CPU时间，也包含带宽/网络时间和存储/IO时间。通过治理机制，将来系统参数是可以调整的，可以改变TGas与1毫秒之间的对应关系。即便如此，上面的内容也是一个不错的开始，让你了解单位gas的意义以及它是怎么得来的。 

**小测验: 1 TeraGas 或者说 TGas 是多少:**

1 TeraGas或TGas等于:  
1 微秒的计算时间  
10 秒的计算时间  
1 毫秒的计算时  
1 纳秒的计算时  

## 常见操作的费用
为了让大家了解NEAR上的费用有个切入点，下面的表格展示一些常见操作，以及目前它们所消耗的TGas，以及对应的NEAR，分别以千分之一NEAR，NEAR为单位。使用的gas价格是1亿个yN。

|操作|TGas|费用(单位mN)|费用(单位Ⓝ)|
|--|--|--|--|
|创建账户|0.42|0.042|4.2⨉10⁻⁵|
|转账|0.45|0.045|4.5⨉10⁻⁵|
|抵押|0.50|0.050|5.0⨉10⁻⁵|
|添加全权key|0.42|0.042|4.2⨉10⁻⁵|
|删除Key|0.41|0.041|4.1⨉10⁻⁵|

# 如何获得NEAR?
## 抵押你的NEAR
POS模型的关键点在于，社区是如何通过抵押而给予验证人支持的。验证人运营节点以支撑起整个网络，因此获得每年5%固定通胀率的NEAR通证奖励，具体是每个周期（约12个小时）创建出一批新的通证。

验证人必须维持一个确保让他们拥有验证人席位的最少抵押数量。通证持有者可以选择一个他们认为能可靠运行网络的验证人去抵押通证，同时按比例获得网络产生的收益。这样就能激励通证持有者持续关注社区!

NEAR钱包已经把用户抵押接口直接集成进了web应用中。

抵押:

1. 在导航条上选择 “Staking” (移动端是下拉框)
2. 点击“Select Validator”按钮
3. 选择一个人验证人
4. 确认你的选择并点击“Stake with Validator”
5. 输入你想要抵押的NEAR数量并点击“Submit Stake”

你需要确认两次交易，第一是选择验证者，第二是向验证者存入权益的数量。

解抵押:

1. 在抵押展示或抵押页面，选择你当前的验证人
2. 点击“Unstake”并确认交易

36到48小时（4个完整的周期）之后，就可以提取权益了。做法是回到验证人页面，点击“Withdraw”。

每周期作为奖励而新生的通证，其产生的大约间隔时间为：  
12 分钟  
12 秒  
12 天  
12 小时  
# 现在呢？我如何与NEAR互动？
接下来如何？如果你已经读到这里，也许会想更深入的了解[NEAR协议](https://learnnear.club/near-protocol-and-solana/). 所以接下来你可以查看[NEAR白皮书](https://near.org/papers/the-official-near-white-paper/). 如果你是个区块链新手，想要了解该领域本身，你可以查看这个视频[解析区块链生态](https://www.youtube.com/watch?v=Y21YtLzGbH0&ab_channel=NEAR).
加入 [NEAR Discord server](https://discord.gg/mxWQjvv8) 逛逛[NEAR论坛](https://gov.near.org/c/learn/33).

原文链接：https://learnnear.club/what-is-near-protocol/
