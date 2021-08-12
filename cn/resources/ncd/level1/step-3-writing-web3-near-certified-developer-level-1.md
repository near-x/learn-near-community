## 步骤3 – 编写 web3（NEAR开发者L1认证）
学习如何在合约中对资金，身份和所有权进行控制。

> :sparkles: 今天的目标是编写可编译的合约。:sparkles: 

确保克隆（clone）每个仓库(repository)并在本地构建。 使每个应用程序运行与阅读代码一样重要，因为今天您将专注于理解所有组件的工作方式

如果由于某种原因而卡在一个应用程序上，只需在Discord中寻求帮助并立即继续。 如果可能的话，请不要等到其他人答复后再继续，否则您会浪费时间。

### :green_book: 核心活动：
在下面的资源部分中，选择AssemblyScript或Rust
* 审查您所选语言标记为“CORE Activity”的3个应用程序

如果您喜欢逐步进行，则可以执行以下操作来仔细研究每个合约或dApp：

1. 从[步骤2](https://learnnear.club/lessons/step-2-reading-web3-near-certified-developer-level-1/) 或步骤3的DAPP（见下文）中选择任何合约
2. 在本地克隆仓库（如果使用Windows，则在Gitpod中克隆）
3. 确保您可以找到合约源代码，并且可以将合约编译为.wasm文件
4. 选择一个您认为可行的方式来测试合约。 您可以使用NEAR CLI命令或运行现有的单元测试或模拟测试。如果有dApp的话，甚至可以使用网页界面来执行测试。
5. **对合约做一点点的修改**。 变化不大，但简单的改动。
6. 重新构建并重新测试（**重复步骤3和4**）
7. 您所做的更改是否按预期进行了？ 还是有什么出错？
8. 需要帮助时，可寻求帮助
9. 不断重复6-7-8，直到您的信心增强……直到您认为自己了解合约并可以控制合约
   10.删除合约，然后从您的笔记中再次写出来（您做笔记了吗？）。 当然，您也可以只重写合约的一小部分。


### :blue_book: 奖励活动：
您看到的应用程序越多，您将对NEAR能做到的事有更多的了解。
1.阅读您所选择的语言的所有应用程序，而不仅仅是3种
2. 还要通读其他语言的所有应用程序。
3. 看看这个小挑战，对您来说可能很有趣
* [Scavenger Hunt Challenge #3](https://hackmd.io/@nearly-learning/hunt-03)

4. 用您喜欢的语言编写一个脚本，该脚本可以自动完成一些乏味的工作。 您将在您已经阅读过的其他项目中找到一些启发。
* 编译一个合约
* 部署合约 (是否初始化可选)
* 调用合约方法


### :orange_book: 更加深入的探索
如果您感到无所畏惧，那么您可能会在一天中做完这些

AssemblyScript
* 在AssemblyScript workshop中完成这些挑战
    - #1. [scavenger hunt](https://github.com/Learn-NEAR/workshop--exploring-assemblyscript-contracts#activityscavenger-hunt) through several AssemblyScript projects
    - #2. [debugging challenge](https://github.com/Learn-NEAR/workshop--exploring-assemblyscript-contracts#activitydebugging-challenge) to fix a few failing unit tests with broken contracts

* 完成这些挑战，然后以一些有趣的方式修改合约
    - #3. [开发周期挑战](https://github.com/Learn-NEAR/workshop--exploring-assemblyscript-contracts#activitydevelopment-lifecycle)将引导您部署一个合约

* 查看NEAR提供的辅助数据结构。 这些都是NEAR Storage的封装，如docs所示 [Storage as seen in docs](https://docs.near.org/docs/concepts/data-storage#docsNav)
-  collections in [near-sdk-as](https://github.com/near/near-sdk-as/tree/master/sdk-core/assembly/collections)
-  collection [performance](https://github.com/near-examples/collection-examples-as)

* 在AssemblyScript中查看同质化和非同质化代币合约
-  [FT](https://github.com/near-examples/FT)
-  [NFT](https://github.com/near-examples/NFT)

Rust
* 完成[workshop on Rust contracts](https://github.com/Learn-NEAR/workshop--berry-club-bot) （基于 [berryclub](https://berryclub.io/)） 来解决失败的测试并绘制一些有意思的去中心化图片
* 查看一些NEAR合约的“convenience”数据结构。 这些都是NEAR Storage的封装, [相关文档](https://docs.near.org/docs/concepts/data-storage#docsNav)
    * 集合[near-sdk-rs](https://github.com/near/near-sdk-rs/tree/master/near-sdk/src/collections)
    * 集合[performance](https://github.com/near-examples/collection-examples-rs)

* 查看同质和非同质代币Rust合约
    * [FT](https://github.com/near-examples/FT)
    * [NFT](https://github.com/near-examples/NFT)
* 查看[berryclub合约](https://github.com/evgenykuzyakov/berryclub)


>调用方法、方法和方法，每天以这种琐碎的速度签署事务，直到记录的块高度的最后一个标记;

>And all our ledgers have hard forked on their way to a dusty death. Out, out, brief consensus!

>web 3’s but a walking shadow, a poor player, that struts and frets his hour upon the internet, and then gossips no more.

>It is a tale told by a HODLer, full of sound and fury, signifying nothing.

>– Willmoon Shakeschain


## :dart: 资源
注意：今天的活动

* 您**需要**构建（并运行测试）每个dApp（“去中心化应用”）
* 您应该**尝试**了解合约中的每一行代码

### AssemblyScript
如果您打算专注于AssemblyScript，请[打开AssemblyScript合约列表](https://airtable.com/shrzKsvgmkM8lvfpp/tblm1quryzSbqBzCK)

您应该至少阅读3个标记为**CORE Activity**合约。


### Rust
如果这是您第一次在计算机上使用Rust时，请参考[文档](https://docs.near.org/docs/tutorials/contracts/intro-to-rust)的介绍。 "3步Rust安装"将帮助您安装所需的软件。

如果您打算专注于Rust，请[打开Rust合约列表](https://airtable.com/shrY5TMWP96L9wSyP/tblm1quryzSbqBzCK)

您应该至少阅读3个标记为**CORE Activity**合约。

您可以阅读有关[Rust合约](https://hackmd.io/@nearly-learning/contract-basics-rust)的更多信息

### 无合约
可以使用NEAR构建不使用合约的应用程序。
以下是这些示例：[无合约示例](https://airtable.com/shr5VqiNCEoPWl0JQ/tblm1quryzSbqBzCK)


## NCDL1 本章作业
现在，是时候提交任务了！
问题1：您读了多少合约？
* 0
* >1

现在，是时候提交任务了！  
问题2:  请提交评论：

合约1：
* 合约的名字
* 你对它感到兴趣的地方是什么
* 理解这个合约哪一部分对您来说是挑战

...

合约N:
* 合约的名字
* 你对它感到兴趣的地方是什么
* 理解这个合约哪一部分对您来说是挑战


原文链接：https://learnnear.club/lessons/step-3-writing-web3-near-certified-developer-level-1/
