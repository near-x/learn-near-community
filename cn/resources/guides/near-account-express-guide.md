# NEAR账户 - 快速指南
## NEAR账户介绍
1. NEAR使用人类可读的账户标识符。例如，maria.near 或 jane.near。
2. 从 NEAR 帐户可以根据需要创建多个子帐户的角度来看，NEAR 帐户系统类似于网站域名系统。 例如，maria.near 的帐户可以创建像 sub.maria.near 帐户，以及first.sub.masha.near, second.sub.maria.near等。
3. NEAR钱包 (https://wallet.near.org/) 、NEAR水龙头(https://faucet.paras.id/)（Ethereum和Metamask用户可以使用）和 near-cli (https://github.com/near/near-cli) （为NEAR集成提供功能的命令行接口）都可以用来创建帐户。
4. 通过 https://nearnames.com 服务，您可以创建一个 NEAR 帐户并的作为礼物发送给朋友或订阅者。
5. 您可以在NEAR浏览器 (https://explorer.near.org/) 以及NEAR的钱包中查看帐户信息。
6. 除了显式帐户（name.near类型），NEAR 生态系统还支持通过 near-cli 创建隐式账户（它们看起来与比特币和以太坊地址相似）。 您可以在此处找到详细的[英文指南](https://docs.near.org/docs/roles/integrator/implicit-accounts)
7. 系统中的每个帐户只能部署1个智能合约。 对于要求用户使用多个智能合约的应用程序，可以使用子帐户来部署。 例如 contract_1.maria.near、contract_2.maria.near等。
8. 在NEAR生态系统中有开发者帐户（https://docs.near.org/docs/concepts/account#dev-accounts）。 他们的专用于测试和调试智能合约。

## NEAR账户 - Keys
1. NEAR和其他大多数区块链一样使用基于密码学的密钥。 它依赖于一对或多对由相互匹配的**公钥（public key**）和**私钥（private key）** 组成的密钥对。
2. NEAR 用户使用公钥进行身份识别，用私钥进行签名交易（在交易创建期间确认帐户所有权）。
3. NEAR 有3种类型的密钥：**Access Keys**用于帐户交易签名，**Validator Keys**允许与网络验证相关的操作，**Node Keys**（网络节点）允许网络上节点之间的底层通信。更多资料介绍可以参考[这里](https://docs.near.org/docs/develop/node/intro/types-of-node)
4. 密钥可以存储在3种不同的存储中：**BrowserLocalStorageKeyStore** - 未加密的本地浏览器存储，用于使用浏览器中的应用程序；**InMemoryKeyStore** - 内存存储，用于临时方案或在本地程序指定特定的密钥； **UnencryptedFileSystemKeyStore** - 用于 near-cli或本地程序，是位于文件系统中的未加密存储。
5. 帐户可以具有多个访问密钥或没有密钥。
6. 密钥可以具有不同的访问级别 - **FullAccess**（完全访问）或 **FunctionCall**（只能调用合约方法）。
7. 所有密钥在一个帐户中是唯一的，但同一个公钥可以以不同访问级别添加到不同帐户上。 访问级别决定了可以使用此密钥执行帐户中的哪些操作。
8. 对于 **FullAccess** 访问级别，所有8种类型的操作均可用：CreateAccountAction（创建帐户）、DeployContractAction（部署合约）、FunctionCallAction（调用合约方法）、TransferAction（将通证发送到另一个帐户）、StakeAction（质押通证）、AddKeyAction（给账户添加密钥）、DeleteKeyAction（删除帐户的某个密钥）、DeleteAccountAction（删除帐户）。
9. 对于 **FunctionCall** 访问级别，只有FunctionCallAction可用（调用合约方法）。 此外，对于这样的密钥，您可以指定它可以调用的合约方法。


Source / 原文链接：https://learnnear.club/near-account-express-guide/
