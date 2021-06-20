# NEAR账户 - 快速指南
## NEAR账户介绍

1. NEAR使用人类可读的账户标识符。例如，maria.near 或 jane.near。

2. NEAR 帐户系统类似于网站域名系统，因为帐户可以根据需要创建多个子帐户。 例如，maria.near的帐户可以创建像sub.maria.near帐户，
以及 first.sub.masha.near, second.sub.maria.near等。

3. NEAR钱包 (https://wallet.near.org/) （NEAR协议钱包），NEAR水龙头(https://faucet.paras.id/)（Ethereum и Metamask用户的水龙头）
   near-cli (https://github.com/near/near-cli) （为NEAR集成提供功能的命令行接口）都可以使用来创建一个帐户。

4. 在NEAR您可以创建一个帐户并在 https://nearnames.com 服务的帮助下将其作为礼物发送给朋友或订阅者。

5. 您可以在NEAR浏览器（https://explorer.near.org/）以及NEAR的钱包中查看帐户信息。

6. 除了可见的帐户（name.near类型），NEAR 生态系统还支持在 near-cli的帮助下建立不可见账户（它们看起来与比特币和以太坊地址相似）。 
   您可以在此处找到详细的[英文指南](https://learnnear.club/doc/roles/integrator/implicit-accounts/)

7. 系统中的每个帐户只能拥有1个智能合约。 对于要求用户使用多个智能合约的应用程序，可以使用子帐户。 例如contract_1.maria.near, 
   contract_2.maria.near等。

8. 在NEAR生态系统中有开发者帐户（https://docs.norg/docs/concepts/accounts#dev-accounts）。 他们的专用于测试和调试智能合约。

## NEAR账户 - Keys

1. NEAR和其他大多数区块链一样基于密码学。 它依赖于由与private key（私钥）匹配的public key（公钥）的密钥对组成。

2. NEAR 用户使用公钥进行身份识别和私钥进行签名交易（在交易创建期间确认帐户所有权）。

3. 在NEAR 有3种类型的keys。[Access keys](https://learnnear.club/docs/concepts/new-to-near/)用于从帐户交易签名，**validator keys**允许与网络验证相关的操作，**node keys**（网络节点）允许网络上节点之间的底层通信。

4. 密钥可以存储在3个不同的存储中。 InMemoryKeyStore - 内存存储，用于临时方案。 BrowserLocalStorageKeyStore - 未加密的本地浏览器存储，
   用于使用浏览器中的应用程序。 UnencryptedFileSystemKeyStore - 在使用near-cli工作时，使用的文件系统中的未加密存储。
   
5. 帐户可以具有零个或多个访问密钥。

6. 密钥可以具有不同的访问级别 - FullAccess（完全访问）或FunctionCall（只能调用合约方法）。

7. 所有密钥在一个帐户中是唯一的，但公钥可以分配给具有不同访问级别的不同帐户。 访问级别决定了可以使用此密钥执行帐户中的哪些操作。

8. 对于 FullAccess 访问级别，所有8种类型的操作可用：CreateAccountAction（创建一个帐户），DeployContractAction（部署合约），FunctionCallAction（调用合约方法），
   TransferAction（将代币发送到另一个帐户），StakeAction（抵押tokens）， AddKeyAction（将一个秘钥添加到帐户），DeleteKeyAction（删除帐户密钥），
   DeleteAccountAction（删除帐户）。

9. 对于FunctionCall访问级别，只有FunctionCallAction可用（调用合约方法）。 此外，对于这样的密钥，您可以指定它可以调用的合约方法。

原文链接：https://learnnear.club/near-account-express-guide/

