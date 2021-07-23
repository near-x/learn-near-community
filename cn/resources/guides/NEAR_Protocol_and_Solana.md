# NEAR Protocol 和 Solana
今天，让我们来认识下世界上最有前途的两个智能合约平台- Near Protocol和Solana。尽管目前Ethereum依旧主导这个市场
但事实是它缺乏可扩展性和高昂的费用迫使大多数开发者寻找可行的替代方案。Near 和 Solana已经成为前两名的领跑者。

## 1.什么是 Solana?
[Solana](https://solana.com/) 成立于2017年，创始人是曾在 DropBox 工作过的 Yakovenko, Eric Williams 以及作为CTO的 Greg Fritzgerald，
创立Solana主要是解决比特币和以太坊目前存在的问题。该项目吸引了来自 Multicoin Capital、 Foundation Capital、 SLOW Capital、 CMCC Global、 Abstract Ventures 等公司的投资。

![img.png](img.png)

Solana区块链的特点
* 每秒50,000次交易和0.4秒的区块产生时间
* 该系统在40 gigabit 网络上每秒可提供2840万次交易
* Solana使用历史证明（Proof-of-History）共识算法


### 历史证明算法是如何运作的？
在一个去中心化的网络中，共识是必不可少的。比特币使用工作证明(proof-of-work，PoW)共识来处理共识。虽然该方法非常安全，
但是很难不忽视它最重要的问题——缺乏可伸缩性。别忘了比特币每秒只能进行7次交易。

Solana使用历史证明算法，通过创造历史记录来证明某一事件发生在某一特定时刻。以下几点需要记住:
* 该算法使用了一个高频可验证延迟函数，该函数需要一定数量的连续步骤来完成
* 在网络中计时的交易或事件将被指定为唯一的散列计数，可以进行公开验证
* 计数允许网络准确地知道交易或事件发生的时间
* 每个节点都有一个用于跟踪网络时间和事件顺序的加密时钟

基于历史证明( PoH)，当使用 GPU 运行时，Solana 网络每秒支持50,000个交易。

### 什么是Solana Cluster?
cluster是一组独立拥有的计算机共同工作，可以被视为一个单一的系统。Cluster的主要特点如下:
* 它们有助于验证未受信任的输出及用户提交的程序
* 维护用户进行的任何交易或事件的记录
* 它保留着有关哪些计算机做了有意义的工作的纪录来维持网络运行
* 它保留着有关真实世界中资产的拥有权的纪录

以下哪项使用了分片？
- Solana
- Near protocol
- Both

### 在 Solana 中编程
Solana 中的智能合约是用 Rust 或 c 编写的，并编译成伯克利包过滤器(BPF)。由于有更多的工具可用，建议您在 Rust 中编写代码。初学者应该使用 Anchor 框架编写程序代码，该框架可以简化执行。

Solana 类似于Linuc操作系统有的文件有一个独特的帐户模型。它们可以保存任何任意数据，还包含关于如何访问它们的元数据。请记住，这些帐户有一个固定的大小，不能调整大小。

Solana目前的编程模型受制于固定的帐户大小，可能会迫使你将应用程序的逻辑部份转移到链下或修改功能以提高效率。
以下哪项是Solana的组成部分？

-Cluster
-Collective
-Parachain


合约例子
```rust
#![feature(proc_macro_hygiene)]

use anchor_lang::prelude::*;
use anchor_spl::token::{self, TokenAccount, Transfer};

#[program]
pub mod plutocratic_hosting {
    use super::*;

    /// Initialize a new contract with initialized content.
    #[access_control(Initialize::validate(&ctx, nonce))]
    pub fn initialize(
        ctx: Context<Initialize>,
        price: u64,
        content: String,
        nonce: u8,
    ) -> ProgramResult {

        // Transfer funds to the contract vault.
        let cpi_accounts = Transfer {
            from: ctx.accounts.from.to_account_info().clone(),
            to: ctx.accounts.vault.to_account_info().clone(),
            authority: ctx.accounts.owner.clone(),
        };
        let cpi_program = ctx.accounts.token_program.clone();
        let cpi_ctx = CpiContext::new(cpi_program, cpi_accounts);
        token::transfer(cpi_ctx, price)?;

        // Initialize the content data.
        let content_record = &mut ctx.accounts.content;
        content_record.price = price;
        content_record.content = content;
        content_record.nonce = nonce;
        content_record.owner = *ctx.accounts.owner.to_account_info().key;
        content_record.vault = *ctx.accounts.vault.to_account_info().key;
        Ok(())

    }

    /// Purchase content address for new price, if transferring more tokens.
    #[access_control(check_funds(&ctx.accounts.content, price))]
    pub fn purchase(ctx: Context<Purchase>, price: u64, content: String) -> ProgramResult {
        // Transfer funds from contract back to owner.
        let seeds = &[
            ctx.accounts.content.to_account_info().key.as_ref(),
            &[ctx.accounts.content.nonce],
        ];
        let signer = &[&seeds[..]];
        let cpi_accounts = Transfer {
            from: ctx.accounts.vault.to_account_info().clone(),
            to: ctx.accounts.owner_token.to_account_info().clone(),
            authority: ctx.accounts.contract_signer.clone(),
        };
        let cpi_program = ctx.accounts.token_program.clone();
        let cpi_ctx = CpiContext::new_with_signer(cpi_program, cpi_accounts, signer);
        token::transfer(cpi_ctx, ctx.accounts.content.price)?;

        // Transfer funds from new owner to contract.
        let cpi_accounts = Transfer {
            from: ctx.accounts.new_owner_token.to_account_info().clone(),
            to: ctx.accounts.vault.to_account_info().clone(),
            authority: ctx.accounts.new_owner.clone(),
        };
        let cpi_program = ctx.accounts.token_program.clone();
        let cpi_ctx = CpiContext::new(cpi_program, cpi_accounts);
        token::transfer(cpi_ctx, price)?;

        // Overwrite content
        let content_record = &mut ctx.accounts.content;
        content_record.price = price;
        content_record.content = content;
        content_record.owner = *ctx.accounts.new_owner.to_account_info().key;

        Ok(())
    }
}

#[account]
pub struct ContentRecord {
    /// Price at which the current content is owned.
    pub price: u64,
    /// Content Data.
    pub content: String,
    /// Public key of current owner of the content.
    pub owner: Pubkey,
    /// Address for token program of funds locked in contract.
    pub vault: Pubkey,
    /// Nonce for the content, to create valid program derived addresses.
    pub nonce: u8,
}

#[derive(Accounts)]
pub struct Initialize<'info> {
    #[account(init)]
    content: ProgramAccount<'info, ContentRecord>,
    #[account(mut, "&vault.owner == contract_signer.key")]
    vault: CpiAccount<'info, TokenAccount>,
    /// Program derived address for the contract.
    contract_signer: AccountInfo<'info>,
    /// Token account the contract is made from.
    #[account(mut, has_one = owner)]
    from: CpiAccount<'info, TokenAccount>,
    /// Owner of the `from` token account.
    owner: AccountInfo<'info>,
    token_program: AccountInfo<'info>,
    rent: Sysvar<'info, Rent>,
}


impl<'info> Initialize<'info> {
    pub fn validate(ctx: &Context<Self>, nonce: u8) -> Result<()> {
        let signer = Pubkey::create_program_address(
            &[
                ctx.accounts.content.to_account_info().key.as_ref(),
                &[nonce],
            ],
            ctx.program_id,
        )
        .map_err(|_| ErrorCode::InvalidNonce)?;
        if &signer != ctx.accounts.contract_signer.to_account_info().key {
            return Err(ErrorCode::InvalidSigner.into());
        }
        Ok(())
    }
}

#[derive(Accounts)]
pub struct Purchase<'info> {
    #[account(mut, has_one = vault)]
    content: ProgramAccount<'info, ContentRecord>,
    #[account(mut)]
    vault: CpiAccount<'info, TokenAccount>,
    #[account(seeds = [
        content.to_account_info().key.as_ref(),
        &[content.nonce],
    ])]
    contract_signer: AccountInfo<'info>,
    #[account(mut, has_one = owner)]
    owner_token: CpiAccount<'info, TokenAccount>,
    #[account(mut)]
    new_owner_token: CpiAccount<'info, TokenAccount>,
    #[account(signer)]
    new_owner: AccountInfo<'info>,
    owner: AccountInfo<'info>,
    token_program: AccountInfo<'info>,
}

fn check_funds(check: &ContentRecord, new_price: u64) -> Result<()> {
    if check.price >= new_price {
        return Err(ErrorCode::InsufficientFunds.into());
    }

    Ok(())
}

#[error]
pub enum ErrorCode {
    #[msg("The given nonce does not create a valid program derived address.")]
    InvalidNonce,
    #[msg("The derived signer does not match that which was given.")]
    InvalidSigner,
    #[msg("Insufficient funds provided to purchase route.")]
    InsufficientFunds,
}
```
合约解释
* 对于每个调用，要访问的所有帐户都用 #[derive(Accounts)]在结构上加注释
* 这些函数初始化所有者和 Purchase 的帐户数据。这使得任何人都可以购买更多的代币
* 临时数据被传递到函数参数中。这些参数位于 initialize 和 purchase 函数内部。这也包括保存交易所需帐户的上下文
* 合约的状态位于 ContentRecord 结构中。使用 #[account]  注解，以表明它代表了账户的数据布局


##  2.什么是 NEAR 协议？
NEAR 协议诞生于 2018 年夏天。 该协议旨在为去中心化应用程序创造完美的环境，它可以提供更高速、更高吞吐量以及与其他链有更好的兼容性。NEAR 有一个独特的分片技术，
它还引入了在 2019 年提出的名为"Doomslug"的区块生成机制。 Doomslug 允许实用确定性或"Doomslug"确定性，确保区块在几秒钟内获得确定性。

NEAR 协议是由 NEAR Collective 开发的，这是一个由开发人员和研究人员合作构建项目的社区。以下是NEAR 的一些关键特性:
* NEAR 是一个分片系统，它支持无限的可伸缩性
* NEAR 是一种易于使用的协议，允许开发人员轻松快速地构建应用程序
* NEAR 不是一个侧链，而是一个Layer-1协议
* 使用 NEAR 创建的 dApps 运行在底层 NEAR 层之上

### 什么是 NEAR Collective
NEAR Collective由不断致力于改进 NEAR 协议的个人组织和其他贡献者组成。 该Collective致力于为 NEAR 网络编写初始代码和進行实践等项目。 NEAR 是完全去中心化的，独立运行，不能被关闭或操纵，即使是那些构建它的人。

这是一个专注于围绕 NEAR 区块链创建一个充满活力的生态系统的非营利组织。它有助于协调治理活动和开发。NEAR Collective有几个项目， NEAR 区块链只是几个项目之一。

NEAR 共识机制
在 NEAR 上实现的共识制称为Nightshade。Nightshade 将系统视为单个区块链。每个区块中所有交易的列表会被拆分为多个碎块，每个碎块中会有一个分片。所有碎块可以组成一个区块，块只可以被维持它的分片状态的节点进行验证。

说到验证，NEAR 的一个关键组件是验证者。这些验证者负责维持在协议内的共识。验证者是专门的节点，它需要保持服务器一直在线，同时保持系统在最新状态。

关于网络验证者，您必须牢记以下几点。
* 每个epoch都会确定它的网络验证者，并根据它们的抵押选择它们
* 已获选的验证者可以通过重新抵押他们的通证和累积的奖励来再次参加。
* 潜在的验证者必须保证他们的抵押保持在一个动态确定的值之上
* 验证者可以使用两种方法来加强他们的权益份额-自己购买通证或通过借用其他人的抵押委托。
* 您得到的回报与您的抵押成正比-抵押越多，奖励越多

这一共识是基于最重权重链共识。这意味着，一旦块生成器发布了一个块，它们将收集验证者节点的签名。然后，块的权重是该块中包含签名的所有签名者的累积。该链的权重是各块权重之和。另外，共识使用了一个确定性小工具，该工具引入了额外的”删除条件”以提高链的安全性。
Doomslug 是哪个协议的区块生成机制?

-Near协议
-Solana
### Aurora and NEAR 协议
Aurora 也在NEAR 协议上推出，提供以太坊第 2 层体验，Aurora 改进 NEAR 的一些方法是:

* 它有助于将吞吐量提高到每秒数千个交易
* 区块的确定性时间为2秒
* 未来生态系统的增长
* 低交易费，比以太坊低1000倍
* 与以太坊永远保持兼容性

代码示例
```rust
use near_sdk::borsh::{self, BorshDeserialize, BorshSerialize};
use near_sdk::collections::LookupMap;
use near_sdk::{env, near_bindgen, AccountId, Balance, Promise};

#[global_allocator]
static ALLOC: near_sdk::wee_alloc::WeeAlloc = near_sdk::wee_alloc::WeeAlloc::INIT;

#[derive(BorshDeserialize, BorshSerialize)]
pub struct ContentRecord {
    pub price: Balance,
    pub content: String,
    pub owner: AccountId,
}

#[near_bindgen]
#[derive(BorshDeserialize, BorshSerialize)]
pub struct ContentTracker {
    values: LookupMap<String, ContentRecord>,
    contract_owner: AccountId,
}

impl Default for ContentTracker {
    fn default() -> Self {
        let contract_owner = env::predecessor_account_id();
        Self {
            values: LookupMap::new(b"v".to_vec()),
            contract_owner,
        }
    }
}

#[near_bindgen]
impl ContentTracker {
    /// Gets content at a given route.
    pub fn get_route(&self, route: String) -> Option<String> {
        self.values.get(&route).map(|v| v.content)
    }

    /// Purchases a route based on funds sent to the contract.
    #[payable]
    pub fn purchase(&mut self, route: String, content: String) {
        let deposit = env::attached_deposit();
        assert!(deposit > 0);
        if let Some(entry) = self.values.get(&route) {
            assert!(
                deposit > entry.price,
                "Not enough deposit to purchase route, price: {} deposit: {}",
                entry.price,
                deposit
            );


            // Refund purchase to existing owner
            Promise::new(entry.owner).transfer(entry.price);
        }


        // Update record for the contract state.
        self.values.insert(
            &route,
            &ContentRecord {
                price: deposit,
                content,
                owner: env::predecessor_account_id(),
            },
        );
    }


    /// Allows owner of the contract withdraw funds.
    pub fn withdraw(&mut self) {
        assert_eq!(env::predecessor_account_id(), self.contract_owner);


        // Send the contract funds to the contract owner
        Promise::new(self.contract_owner.clone()).transfer(env::account_balance());
    }
}

```

合约解释
* 该合约由 ContentTracker 中的 #[near_bindgen] 定义，它类似于 Solidity 中的构造函数，并在部署合约时调用
* purchase函数 使用了  #[payable] 注解
* 合约包括以 Promise: : new (...) . transfer (...) ; lines 的形式进行的异步调用
* 数据结构 LookupMap < String，ContentRecord > 处理键值查找，它访问存储，这等同于 soliity“ mapping”

## 3.总结
Solana 和 NEAR 协议都是卓越的智能合约平台，已经建立了高度活跃的社区。他们都带来了特殊的功能，帮助解决去中心化最大的问题-速度。
这两个平台都在不断成长，并且前景看好。


原文链接：https://learnnear.club/near-protocol-and-solana/
