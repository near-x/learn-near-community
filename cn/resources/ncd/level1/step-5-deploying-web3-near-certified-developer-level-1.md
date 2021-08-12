## 步骤5 – 部署 web3（NEAR开发者L1认证）
学习将智能合约部署到TestNet。

>今天的目标是部署合同并验证其是否有效。

当我们在NEAR上说“application”时，通常是指有以下行为的软件：
* （a）控制的链上数据和行为的智能合约（如NFT合约）
* （b）控制链下数据和行为并与智能合约进行通信的应用（如web应用）

在这个星期，我们研究了许多合约和应用程序，现在我们将部署它们。

MainNet的部署超出了课程的范围，因此我们将重点关注TestNet，以及作为额外活动，您可以在LocalNet中私下构建合约。 在TestNet上运行的所有内容都应在MainNet上同样有效。 实际上，这是TestNet的唯一目的：在我们将合约发布到MainNet上之前，为我们提供工作的完整预览。

### :green_book: 核心活动：
1. 填写下面的表格，以预约您的演示。 您必须（与团队或您自己）参与演示的开发以获得证书。
	如果您的演示是单独的（仅您一个），请在下面的表格中填写您的信息。 如果您的演示是团队（您和其他人），则仅在下面填写表格，并包括团队中所有人员的姓名。
   [ REGISTER for your demo slot ](https://learnnear.club/lessons/step-5-deploying-web3-near-certified-developer-level-1/#Submit%20Demo)
   > 为了获得证书，您必须在课程的最后发表您的演示。 如果您现在还没有准备好演示，那么欢迎您在**下个月的最后一个周五**发表演示

2. 将至少一个应用程序部署到TestNet
	* 选择您在第1天和第2天看到的合约和应用程序中的任何一个（或多个）。部署时，应用程序是用Rust还是AssemblyScript编写都没有关系。 所有合约代码都编译为WebAssembly，并部署到网络以在Wasm兼容虚拟机中运行。
   对于大多数应用程序，您将使用诸如yarn dev之类的命令，但是您也可以使用NEAR CLI[near dev-deploy](https://docs.near.org/docs/tools/near-cli#near-dev-deploy) 轻松部署应用程序，并使用[near dev-deploy](https://docs.near.org/docs/tools/near-cli#near-dev-deploy) 部署到TestNet（或者如果您已经有了帐户，则[near deploy](https://docs.near.org/docs/tools/near-cli#near-deploy) ）。
	  
3. 验证已经部署的应用程序
   使用[NEAR Explorer](https://explorer.testnet.near.org/)验证部署（将部署的证据找到合约已部署到的目标帐户）
   使用NEAR CLI 的命令[near state <contract-account>](https://docs.near.org/docs/tools/near-cli#near-state) ，成功部署后的code_hash返回值将不是空值（全1）

5. 对应用程序的使用验证
   使用[NEAR Explorer](https://explorer.testnet.near.org/) 验证部署（查找与[您的帐户](https://explorer.testnet.near.org/accounts/sherif.testnet) 与部署合约的目标帐户相关的任何交易的记录）


### :blue_book: 奖励活动：
如果您还有时间和精力，还有更多内容等待您

1. 安装[nearup](https://github.com/near/nearup) 获得一个[本地节点运行](https://github.com/near/nearup#spawn-a-local-network) 。 这将包括：
* 安装nearup和nearcore依赖
* 编译nearcore（这可能需要很长时间）
* 运行nearup使用签名编译的nearcore二进制文件

2. 确保您通过阅读nearup文档（git仓库的README）以了解设置的详细信息。
3. 您最终将使用4节点LocalNet。 要创建帐户，您必须在验证节点之一的主目录中找到的验证节点keys（下面是来自MacOS）
   这是LocalNet keystore文件系统中的位置
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
		    
### :orange_book: 更加深入的探索
如果您感到无所畏惧，那么您可以在一天中做完这些

现在该准备demo了！

演示demo提交
项目名称*
邮箱*
项目团队成员*
github仓库地址*

原文链接：https://learnnear.club/lessons/step-5-deploying-web3-near-certified-developer-level-1/
