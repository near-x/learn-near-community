## 步骤4 – 测试 web3（NEAR开发者L1认证）
学习编写智能合约的单元测试和模拟测试。

> 今天的目标是编写可以合约的单元测试和模拟测试。

核心活动：
在下面的资源章节中，选择AssemblyScript或Rust
* 为标记为“CORE Activity”的3个合约写上3~5个单元测试

奖励活动
如果您还有时间和精力，还有更多内容等待您

如果您需要更多有关此挑战的想法，请考虑以下事项：
1. 查找没有单元测试的合约（有很多）并编写它们
2. 从合约中删除一些（或全部）现有的单元测试并重写它们。
3. 看看这个小难题，对您来说可能很有趣
* [Scavenger Hunt Challenge #4](https://hackmd.io/@nearly-learning/hunt-04)
4. 从空白文档（或只是模板代码）开始，然后尝试测试驱动（TDD）合约。


更加深入的探索
如果您感到无所畏惧，那么您可以在一天中做完这些

模拟测试是一项不断发展演进的工作，我们为您提供了一些示例帮助。 了解NEAR上的模拟测试的关键在于测试**Wasm二进制文**件。 这意味着相同的模拟测试配置将适用于Rust和AssemblyScript。

实际上，可以对已编译的Rust或已编译的AssemblyScript合约使用完全相同的模拟测试。 一旦您考虑到模拟测试使用的是相同的链上虚拟机，就恨容易理解。因此您在模拟测试中所做的一切都应该在1：1链上虚拟机可重复的。

注意，模拟测试必须用Rust写。 以下示例可以帮助您理解。
* [NEARly Neighbors](https://learn-near.github.io/nearly-neighbors) 有模拟测试
* [Workshop on Cross-contract Calls](https://bit.ly/near-xcc) 有模拟测试

>What is a new idea — what Satoshi figured out — is how to independently agree upon a history of events without central coordination. He found a way to implement a decentralised timestamping scheme that:
> 
> a) doesn’t require a time-stamping company or server,
> b) doesn’t require a newspaper or any other physical medium as proof, and
> c) can keep the ticks more-or-less constant, even when operating in an environment of ever-faster CPU clock times.
> – Gigi in Bitcoin is Time
>

## 资源
注意：今天的活动

* 您**确实**需要构建（并运行测试）（如果可以）每个dApp（“去中心化应用”）
* 您应该**尝试**了解合约中的每一行代码

### AssemblyScript
如果你想专注于AssemblyScript，[ OPEN the list of AssemblyScript contracts ](https://airtable.com/shrG4kGx80F55usI4)

至少3份被标记为核心活动的合同

a)为每个合约编写3-5个新的单元测试，不管它是否已经有单元测试

b)验证测试如预期通过(测试可以通过命令行运行)

单元测试是由[as- aspect](https://github.com/jtenner/as-pect)提供的，语法类似于RSpec。这个库有很好的[文档](https://tenner-joshua.gitbook.io/as-pect/)记录，但有时[tests for the testing library](https://github.com/jtenner/as-pect/tree/master/packages/assembly/assembly/__tests__)可能是帮助您快速学习的示例的最佳来源。

[near.dev](https://examples.near.org/) 上几乎所有可用的示例都包括单元测试。
 

### Rust
如果您打算专注于Rust，请[打开Rust合约列表](https://airtable.com/shrY5TMWP96L9wSyP/tblm1quryzSbqBzCK)

至少3个标记为**CORE Activity**合约。
* a）为每个合约写3-5个新的单元测试，无论是否有单位测试
* 按预期验证测试通过（测试可以通过IDE或命令行运行）

单元测试包括Rust语言的一部分。

您可以通过[Rust by Example](https://doc.rust-lang.org/rust-by-example/testing/unit_testing.html) 或 [“the book”](https://doc.rust-lang.org/book/ch11-01-writing-tests.html) 阅读更多有关单位测试。

如果您想看到一些更好的例子,所有NEAR的[核心合约](https://github.com/near/core-contracts) 都包括单元测试。 例如，您可以看白名单合约。例如，[test_utils](https://github.com/near/core-contracts/blob/master/whitelist/src/tests/test_utils.rs#L21)，该导入设置单元测试MockedBlockchain上下文，为每个独立的文件

原文链接：https://learnnear.club/lessons/step-4-testing-web3-near-certified-developer-level-1/