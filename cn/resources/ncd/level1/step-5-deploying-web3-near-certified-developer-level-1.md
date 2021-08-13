# 第 5 步 - 部署 web3 - NEAR 认证开发者（一级）

_学习将智能合约部署到TestNet。_

--------
> :sparkles: 今天的目标是部署合约并验证其是否有效。
--------

* 当我们在NEAR上说“应用”时，通常是指有以下行为的软件：
   * （a）控制**链上**数据和行为的**智能合约**（如NFT合约）
   * （b）控制**链下**数据和行为并**与智能合约进行通信**的应用（如web应用）

在这个星期，我们研究了许多合约和应用程序，现在我们将部署它们。

MainNet的部署超出了课程的范围，因此我们将重点关注TestNet，以及作为额外活动，您可以在私下构建的LocalNet上部署。 在TestNet上运行的所有内容都应在MainNet上同样有效。 实际上，这是TestNet的唯一目的：在我们将合约发布到MainNet上之前，为我们提供工作的完整预览。

### :green_book: 核心活动

1. 填写下面的表格，**以预约您的演示时间**。您**必须**（与团队一起或独自一人）参与演示项目的开发从而获得**证书**。如果只有您一个人参加演示，那么在下面的表格中填写您个人的信息即可。 如果您有一个团队，在下面的表格中请填入团队所有人员的信息（仅需提交一份表格）。[**预约您的演示时间**](https://learnnear.club/lessons/step-5-deploying-web3-near-certified-developer-level-1/#Submit%20Demo)

   > _为了获得证书，您**必须**在课程的最后进行您的演示。如果您现在还没有准备好演示，那么欢迎您在**下个月的最后一个周五**进行演示。_

2. 将至少一个应用部署到TestNet

	- 选择您在第1天和第2天看到的合约和应用程序中的任何一个（或多个）。部署时，应用程序是用Rust还是AssemblyScript编写都没有关系。所有合约代码都编译为WebAssembly，并部署到链上以在Wasm兼容虚拟机中运行。
   对于大多数应用程序，您将使用诸如`yarn dev`之类的命令，但是您也可以使用NEAR CLI[`near dev-deploy`](https://docs.near.org/docs/tools/near-cli#near-dev-deploy) 轻松部署应用程序到Testnet（或者如果您已经有了Mainnet帐户，则使用[`near deploy`](https://docs.near.org/docs/tools/near-cli#near-deploy) ）。
	  
3. 验证已经部署的应用

   - 使用[NEAR Explorer](https://explorer.testnet.near.org/)验证部署（找到合约被部署到[目标账户](https://explorer.testnet.near.org/accounts/dev-1614258294715-7729054)的凭证）
   - 使用NEAR CLI 的命令[`near state <contract-account>`](https://docs.near.org/docs/tools/near-cli#near-state) ，成功部署后的`code_hash`返回值将不是默认值（全1）

4. 验证使用你的应用

   - 使用[NEAR Explorer](https://explorer.testnet.near.org/) 验证部署（在[您的帐户](https://explorer.testnet.near.org/accounts/sherif.testnet) 上查找与已部署合约的目标账户相关联的交易记录）


### :blue_book: 奖励活动

_如果您还有时间和精力，还有更多内容等待您_

1. 安装[nearup](https://github.com/near/nearup) 获得一个[本地节点运行](https://github.com/near/nearup#spawn-a-local-network)。 具体步骤为：

   * 安装nearup和nearcore依赖
   * 编译nearcore（这可能需要很长时间）
   * 运行nearup（使用刚刚编译的nearcore二进制文件）

2. 确保您通过阅读`nearup`文档（代码仓库的README）了解配置的详细信息。
3. 您最终将使用4节点LocalNet 要创建帐户，您必须在验证节点之一的机器上找到的验证节点密钥（下面是MacOS的目录形式）

---

这是LocalNet keystore在文件系统中的样子：

```bash
/Users/sherif/.near/localnet
├── node0
│   ├── config.json
│   ├── data
│   ├── genesis.json
│   ├── node_key.json
│   └── validator_key.json  <-- open one of these files
├── node1
│   ├── config.json
│   ├── data
│   ├── genesis.json
│   ├── node_key.json
│   └── validator_key.json
├── node2
│   ├── config.json
│   ├── data
│   ├── genesis.json
│   ├── node_key.json
│   └── validator_key.json
└── node3
   ├── config.json
   ├── data
   ├── genesis.json
   ├── node_key.json
   └── validator_key.json
```
		    
### :orange_book: 深入探索

_如果您感到无所畏惧，那么您可以在一天中做完这些_

现在该准备demo了！

演示demo提交

项目名称 *

邮箱 *

项目团队成员 *

GitHub代码仓库 *

提交



原文链接：https://learnnear.club/lessons/step-5-deploying-web3-near-certified-developer-level-1/
