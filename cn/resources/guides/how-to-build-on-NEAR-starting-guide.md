# 如何构建NEAR - 开始指南
## 前置知识
* 阅读 [什么是NEAR](https://learnnear.club/what-is-near/)
* 具备JavaScript开发经验

开发者是区块链生态系统中的命脉。 为了使区块链技术被主流采纳，它需要降低开发人员的进入的门槛，并允许他们为大众创造有趣而成熟的应用程序。
因此，NEAR合约支持使用和JavaScript非常相似的 **AssemblyScript** 来编写。

所以，如果您在NEAR上开发构建，您可以使用以下工具
* JavaScript SDK: 处理任何由JS上下文到NEAR网络的连接、签名、交易，以及部署
* Rust Contract SDK: 建立安全，稳定的合约以管理高价值的资产
* AssemblyScript Contract SDK: 利用JS语法以零障碍的方式去学习及建立原型
* JSON RPC API: 所有与平台的通信都通过此API
* Command Line Interface: 开发人员和验证者的全功能命令行工具包
* NEAR Explorer（浏览器）: 一个区块链搜索工具，允许开发人员查看交易详细信息、帐户信息、区块详细信息等
* NEAR Wallet: 提供对普通用户友好的界面来创建帐户、管理访问密钥等
* nearup: 在本地管理部署以及加入公共或私人网络
* Rainbow Bridge （彩虹桥）: 快速的跨链操作、安全的互操作性
* EVM: 以太坊兼容的虚拟机

现在，让我们开始第一步吧。

## 简要概述
在NEAR上的应用分两个不同的部分 - 后端和前端。

* 智能合约（后端）：在链中存储和修改数据。 合约需要提供一些允许用户“查看”或“更改”状态的方法。
* 与智能合约的互动（前端）：您可以与您自己或者其他人部署的合约互动。 对于相关的互动，您可以通过在应用程序中使用near-api-js源码中的[快速开始](https://github.com/near/near-api-js/blob/master/examples/quick-reference.md) 和[Code Snippets](https://github.com/near/near-api-js/tree/master/examples/cookbook) 进行操作。

<Question1> 
NEAR上的应用程序分成两个不同的部分 - 后端和前端。 后端是______
- 主网（Mainnet）
- 测试网（Testnet）
- 智能合约
</Question1>

**如何构建和调用智能合约**
NEAR当前支持
* **Rust – near-sdk-rs**: 一组封装，提升了用Rust编程语言编写合约的安全性，以实现高价值的合约
* **AssemblyScript near-sdk-as**: 一组工具，使用它编写的智能合约看起来像 TypeScript，并编译为WASM执行

> 注意: 由于语言和编译工具的新颖性，目前AssemblyScript不建议在金融应用的生产环境中使用。

现在，让我们开始吧。

## 设置测试网

在NEAR创建帐户的最简单方法是透过[NEAR Wallet](https://wallet.near.org/)。 需要注意的是，NEAR有几个独自运行的网络环境（如主网、测试网等），他们有各自独立的账户，例如，你在主网创建的账户，并不能在测试网上使用。 
现在，按照步骤创建钱包。 并且确保您已遵循所需步骤来进行了安全备份。

>注意：在mainnet上创建帐户几乎与testnet相同，但需要为该帐户进行初始资金。 以下是mainnet帐户创建指南。

在部署时，无论应用程序以Rust还是AssemblyScript编写，所有合约代码都被编译为WebAssembly并部署到网络，以在WASM兼容的虚拟机内运行。
像大多数应用程序一样，在开发时您可以使用的 `yarn dev` 命令，然后您可以使用 NEAR CLI 命令 `near dev-deploy` 轻松部署应用程序到TestNet（如果已创建了自己的帐户，也可以使用 `near deploy` 命令）。

<Question2> 
所有合约代码都被编译为WebAssembly并部署到网络，从而运行在____ 里面？
- 沙盒（Sandbox）
- WASM兼容虚拟机
- 以太坊虚拟机（EVM）
</Question2> 


现在，执行以下操作：
1. 在NEAR浏览器中查看。 在这里，您可以搜索在NEAR产生的所有交易和区块。 尝试搜索刚刚创建的帐户，并查看您已创建的交易。
2. 现在安装[near-cli](https://docs.near.org/docs/tools/near-cli#docsNav)。 这是一个命令行接口，允许您与NEAR无缝交互。 此文档包含了所有的near-cli命令及相关示例。
3. 尝试运行您的第一个命令：[near login](https://docs.near.org/docs/tools/near-cli#near-login)。 您将重定向到您的NEAR钱包，并在本地保存您的testnet帐户秘钥。

在了解了testnet后，您也可以随时运行本地节点。 但是，如果您只想练习代码，那么我们建议您使用testnet。

## 如何运行一个NEAR节点？
与任何基于区块链的生态系统一样，[NEAR协议](https://learnnear.club/near-protocol-and-solana/)在一群公开的计算机(或“节点”)上运行。

您可出于以下几个原因决定是否运行您自己的节点：
* 在MainNet，TestNet或Betanet的节点上开发和部署合约
* 在本地（独立和隔离）节点上开发和部署合约（有时称为“LocalNet”）。
* 加入网络成为运行“验证节点”的验证者

您可以通过安装NEAR betanet和testnet节点。通过[https://github.com/near/nearup](https://github.com/near/nearup) 获取指导 

<Question3> 
与任何区块链的生态系统一样，NEAR协议在一个名为____ 的一群公开的计算机上运行?
- 节点（Nodes）
- 区块链
- NEAR 协议
</Question3> 

## 使用Docker运行官方节点
默认情况下，NEAR 使用Docker运行客户端。 所以，你所做的第一件事是安装Docker和nearup。 然后运行：
```bash
nearup betanet
```
（如果您更喜欢使用TestNet，那么只需在上面的命令用testnet替换betanet）

接下来，提示您输入帐户ID。 如果您不是要做验证者，则可以留空。否则，验证者应在这里输入您想要抵押的帐户的ID：
```bash
Enter your account ID (leave empty if not going to be a validator)
```

现在，您的Docker节点开始运行在后台中。 要检查Docker内的日志，请运行 docker logs –follow nearcore 。

## 在 NEAR 上创建一个简单的代码
NEAR有一个有用的程序或[示例代码](https://examples.near.org/)列表，可以很方便的checkout。 因此我们将checkout的代码是[Guest Book](https://examples.near.org/guest-book)。使用该程序允许您登录NEAR并向留言簿添加消息！ 使用AssemblyScript后端和React前端构建的starter应用程序。

## 学习Guest Book代码
要在本地运行此项目，您需要确保以下内容。

* 确保安装了Node.js≥12（https:/nodejs.org）， 然后使用它来安装yarn：npm install –global yarn（或npm i -g yarn）
* 安装依赖：yarn install (或 just yarn)
* 运行本地开发服务器：yarn dev（请参阅package.json获取您可以使用yarn运行的完整参数列表）

现在您可以拥有一个由NEAR TestNet支持的本地开发环境! 统一运行`yarn dev`，它会返回相关的网址，您可以通过浏览器看到相关的应用程序。

[GitHub页面](https://github.com/near-examples/guest-book)。

您可能会发现[此视频](https://www.youtube.com/embed/B6Gc_OQjX9E?feature=oembed)也很有用。

### 探索代码
正如您所看到的，代码分成前端和后端：

* 后端代码在/assembly文件夹中。运行yarn deploy:contract，将部署该合约到NEAR区块链。 这是一个NEAR智能合约。
* 前端代码在/src文件夹中。/src/index.html是开始探索的位置。请注意，它在/src/index.js中加载，您可以在其中学习前端如何连接到NEAR区块链。

## 后端代码
### #1 合约的数据模型： assembly/model.ts

```ts
import { context, u128, PersistentVector } from "near-sdk-as";
/** 
 * Exporting a new class PostedMessage so it can be used outside of this file.
 */
@nearBindgen
export class PostedMessage {
  premium: boolean;
  sender: string;
  constructor(public text: string) {
    this.premium = context.attachedDeposit >= u128.from('10000000000000000000000');
    this.sender = context.sender;
  }
}
/**
 * collections.vector is a persistent collection. Any changes to it will
 * be automatically saved in the storage.
 * The parameter to the constructor needs to be unique across a single contract.
 * It will be used as a prefix to all keys required to store data in the storage.
 */
export const messages = new PersistentVector<PostedMessage>("m");
```
分析

@nearBindgen将类标记为序列化。Serializable 是一个用于“标记”类的接口，以使这些类的对象可能获得某个功能。

“PostedMessage”类有三个成员:
* premium - 可以标记带有附加 NEAR 通证的讯息
* sender - 可以追踪留言簿上讯息的签名者
* text - 可以储存留言簿讯息

最后，“messages”是一个集合，存储在new PersistentVector<PostedMessage> 结构中。

### #2 合约的行为 :  assembly/main.ts
```ts
import { PostedMessage, messages } from './model';
// --- contract code goes below
// The maximum number of latest messages the contract returns.
const MESSAGE_LIMIT = 10;
/**
 * Adds a new message under the name of the sender's account id.\
 * NOTE: This is a change method. Which means it will modify the state.\
 * But right now we don't distinguish them with annotations yet.
 */
export function addMessage(text: string): void {
  // Creating a new message and populating fields with our data
  const message = new PostedMessage(text);
  // Adding the message to end of the the persistent collection
  messages.push(message);
}
/**
 * Returns an array of last N messages.\
 * NOTE: This is a view method. Which means it should NOT modify the state.
 */
export function getMessages(): PostedMessage[] {
  const numMessages = min(MESSAGE_LIMIT, messages.length);
  const startIndex = messages.length - numMessages;
  const result = new Array<PostedMessage>(numMessages);
  for(let i = 0; i < numMessages; i++) {
    result[i] = messages[i + startIndex];
  }
  return result;
}
```

分析
MESSAGE_LIMIT用于避免无限的调用（例如: 可能昂贵的）来检索来自存储Guest Book的讯息

我们还在本合约中使用两个不同的公开方法 - addMessage() 和getMessages()

                                 
## 前端代码
### #1 网络配置:  src/config.js
```js
const CONTRACT_NAME = process.env.CONTRACT_NAME || 'guest-book.testnet';
function getConfig(env) {
  switch(env) {
    case 'mainnet':
      return {
        networkId: 'mainnet',
        nodeUrl: 'https://rpc.mainnet.near.org',
        contractName: CONTRACT_NAME,
        walletUrl: 'https://wallet.near.org',
        helperUrl: 'https://helper.mainnet.near.org'
      };
    // This is an example app so production is set to testnet.
    // You can move production to mainnet if that is applicable.
    case 'production':
    case 'development':
    case 'testnet':
      return {
        networkId: 'default',
        nodeUrl: 'https://rpc.testnet.near.org',
        contractName: CONTRACT_NAME,
        walletUrl: 'https://wallet.testnet.near.org',
        helperUrl: 'https://helper.testnet.near.org'
      };
    case 'betanet':
      return {
        networkId: 'betanet',
        nodeUrl: 'https://rpc.betanet.near.org',
        contractName: CONTRACT_NAME,
        walletUrl: 'https://wallet.betanet.near.org',
        helperUrl: 'https://helper.betanet.near.org'
      };
    case 'local':
      return {
        networkId: 'local',
        nodeUrl: 'http://localhost:3030',
        keyPath: `${process.env.HOME}/.near/validator_key.json`,
        walletUrl: 'http://localhost:4000/wallet',
        contractName: CONTRACT_NAME
      };
    case 'test':
    case 'ci':
      return {
        networkId: 'shared-test',
        nodeUrl: 'https://rpc.ci-testnet.near.org',
        contractName: CONTRACT_NAME,
        masterAccount: 'test.near'
      };
    case 'ci-betanet':
      return {
        networkId: 'shared-test-staging',
        nodeUrl: 'https://rpc.ci-betanet.near.org',
        contractName: CONTRACT_NAME,
        masterAccount: 'test.near'
      };
    default:
      throw Error(`Unconfigured environment '${env}'. Can be configured in src/config.js.`);
  }
}
module.exports = getConfig;
```
分析
上面的代码定义了连接到NEAR网络所需的数据和端点。这里定义的连接信息包括MainNet，TestNet和Betanet以及默认LocalNet配置

### #2 配置 :  src/index.js
```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import getConfig from './config.js';
import * as nearAPI from 'near-api-js';
// Initializing contract
async function initContract() {
    const nearConfig = getConfig(process.env.NODE_ENV || 'testnet');
    // Initializing connection to the NEAR TestNet
    const near = await nearAPI.connect({
        deps: {
            keyStore: new nearAPI.keyStores.BrowserLocalStorageKeyStore()
        },
        ...nearConfig
    });
    // Needed to access wallet
    const walletConnection = new nearAPI.WalletConnection(near);
    // Load in account data
    let currentUser;
    if(walletConnection.getAccountId()) {
        currentUser = {
            accountId: walletConnection.getAccountId(),
            balance: (await walletConnection.account().state()).amount
        };
    }
    // Initializing our contract APIs by contract name and configuration
    const contract = await new nearAPI.Contract(walletConnection.account(), nearConfig.contractName, {
        // View methods are read-only – they don't modify the state, but usually return some value
        viewMethods: ['getMessages'],
        // Change methods can modify the state, but you don't receive the returned value when called
        changeMethods: ['addMessage'],
        // Sender is the account ID to initialize transactions.
        // getAccountId() will return empty string if user is still unauthorized
        sender: walletConnection.getAccountId()
    });
    return { contract, currentUser, nearConfig, walletConnection };
}
window.nearInitPromise = initContract()
    .then(({ contract, currentUser, nearConfig, walletConnection }) => {
        ReactDOM.render(
            <App
                contract={contract}
                currentUser={currentUser}
                nearConfig={nearConfig}
                wallet={walletConnection}
            />,
            document.getElementById('root')
        );
    });
```

分析
这是前端部分，配置连接到NEAR网络。 需要通过注入钱包的连接及连接双方合约的方法（methods）来配置合约接口。

## 部署一个智能合约
NEAR的每个智能合约都有自己的相关帐户。运行yarn dev时，您的智能合约将使用一个自动生成的开发账户部署到NEAR TestNet上。如果您现在想要使其持久化，以下是您要做的。
### Step 0: 安装near-cli
以下是全局安装near-cli的方法
```bash
npm install --global near-cli
```
该命令会安装near CLI工具。 检查是否安装成功：
```bash
near --version
```
### Step 1: 为合约创建一个账号
访问NEAR 钱包并制作新帐户。将这些智能合约部署到此新帐户。

按照为您提供的提示说明，现在登录并授权NEAR CLI使用此新帐户：
```bash
near login
```
### Step 2: 设置合约名字
修改在src/config.js中设置合约帐户名称。将其设置为您在上面使用的帐户ID。
```js
const CONTRACT_NAME = process.env.CONTRACT_NAME || 'your-account-here!'
```
### Step 3: 修改URL
如果您选择"Fork"以建立仓库的分叉，则需要将远程URL更改为您具有“commit”权限的仓库(repo)。 这将允许从命令行进行自动部署到GitHub页面。
```bash
$ `git remote set-url origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git`
```
### Step 4: 部署！
您只需要以下命令即可部署智能合约：
```bash
yarn deploy
```
此命令做两件事：
* 构建和部署智能合约到 NEAR TestNet
* 可以通过使用gh-pages构建并部署前端合约代码到Github。 此方式适合已经在github上建立仓库的情况。 可随时修改package.json中的部署脚本更改部署的位置。

<Question4> 
每个在NEAR上的智能合约，都有自己相关联的____?
- 通证
- 钱包
- 账户
- 以上所有
</Question4> 


## 下一步
至此，您知道了如何运行基本代码，如果您想要深入了解NEAR，请查看NEAR的[开发者文档](https://docs.near.org/docs/develop/basics/getting-started)。


原文链接：https://learnnear.club/how-to-build-on-near-starting-guide/
