# NEAR彩虹桥是如何工作的
原作者 Matt Henderson of [Aurora](https://aurora.dev/blog/2021-how-the-rainbow-bridge-works).

The NEAR Rainbow Bridge is unique in crypto as the only permission-less, trustless bridge to Ethereum. In this article, we’re going to demystify how it works!

The NEAR Protocol created the [Rainbow Bridge](https://ethereum.bridgetonear.org/)—something that’s both unique and valuable in the crypto space, a fully “trustless” bridge for transferring tokens between Ethereum and NEAR—and ultimately, Aurora. While there are technical descriptions of the bridge out there, this article will explain how it works in a way hopefully understandable by anyone with a basic familiarity with crypto.

## The concept
Let’s start by just imagining that I want to transfer 20 DAI from [Ethereum to NEAR](https://learnnear.club/near-ethereum/). Since physical transfer of tokens isn’t possible between networks, this means we need to take 20 DAI out of circulation on Ethereum, and put 20 DAI into circulation on NEAR, so that the global supply of DAI doesn’t change.

Here’s how I could do that in a trustless, permissionless way:

1. I tell the Ethereum network that I want to transfer 20 DAI somewhere else.
2. The Ethereum network locks my 20 DAI in a vault (a smart contract), so that they are taken out of circulation.
3. Once I’m certain those 20 DAI have been locked on Ethereum, I then tell NEAR to create 20 new DAI for me there.
4. NEAR doesn’t trust me, of course, and so it asks me to prove that I’ve locked 20 DAI on Ethereum.
5. I provide NEAR with proof that I’ve locked those DAI on Ethereum.
6. NEAR independently verifies my proof, and then creates 20 new DAI for me to use on NEAR.


Later, if and when I wish to move my DAI from NEAR back to Ethereum, I simply reverse the above procedure. Neat, huh?

## The actors
So now let’s look at how all that happens in practice, using the Rainbow Bridge. The story is going to involve a number of technical components that make up the bridge:

**The Rainbow Bridge UI** — this is [the website](https://ethereum.bridgetonear.org/) where you, as a user, interact with the bridge to transfer your assets between networks.

**The LiteNode** — This is like a blockchain node, except that it only stores block headers, dramatically reducing the storage space needed. The LiteNode is implemented as a smart-contract, and we have two of them—one deployed on the Ethereum network, which stores NEAR block headers, and one deployed on NEAR which stores Ethereum block headers.

(Just an FYI, the LiteNode is actually referred to as the “light client” in other articles, for historical reasons. If you ask me, “What stores blockchain data?”, my first thought is “a node”, and so in this article, to help with mental models, I’m calling it the LiteNode.)

**Relayers** — Since LiteNodes are smart contracts, they can’t run and update themselves. Relayers are scripts running on traditional servers, that periodically read blocks from one blockchain, and communicate them to the LiteNode running on the other. So the relayers keep the LiteNodes up-to-date.

Since there is a transaction cost—i.e. gas fees—each time a relayer updates a LiteNode, the one on NEAR (containing the Ethereum blocks) is updated on each Ethereum block (since NEAR gas fees are cheap), while the update frequency on Ethereum (containing the NEAR blocks) is configurable and determined by an economic budget (currently about 12 to 16 hours).

**Connectors** — Connectors are smart contracts responsible for all of the logic associated with the cross-chain management of a given asset type. Like LiteNodes, they exist in pairs—one running on Ethereum, and one running on NEAR. For example, there is a pair of “ETH Connectors” responsible for transferring ETH between the two networks. And there’s an “ERC-20 Connector” pair responsible for transferring ERC-20 tokens. Someone could write an “NFT” Connector, “Prediction Market Outcomes” Connector or “DAO Vote Results” Connector if they wished. Any asset or data can be transferred across the Rainbow Bridge, if relevant Connectors exist!

## Putting the pieces together
To understand how all these elements work together to allow me to permissionlessly, and trustlessly, transfer tokens between Ethereum and NEAR, let’s walk through our original example again:

1. Using the **Rainbow Bridge UI**, I start a transfer of 20 DAI from Ethereum to NEAR.
2. When I confirm the first of two transactions in [MetaMask](https://metamask.io/), the Rainbow Bridge communicates with the **ERC-20 Connector** on Ethereum (since DAI is an ERC-20 token), which transfers and locks 20 DAI in its vault. These DAI are then no longer in circulation on the Ethereum network.
3. Based on the header data in my transaction block, the **Rainbow Bridge UI** calculates a **cryptographic “proof”** that I really did lock 20 DAI.
4. Since we’re next going to ask the NEAR network to create some DAI based on what just happened on Ethereum, we first wait for the **Relayer** to send about 20 Ethereum block headers to the **LiteNode** running on NEAR. This is for security, in the same way your crypto exchange makes you wait for some confirmations before using your deposited funds.
5. After this wait, the **Rainbow Bridge UI** then allows us to take step two in the process—asking the **ERC-20 Connector** on NEAR to create 20 new DAI for us on the NEAR network.
6. When we make this request of the ERC-20 Connector, we provide our **cryptographic proof** we received earlier, “proving” that we locked 20 DAI on Ethereum.
7. The **ERC-20 Connector** on NEAR will then lookup our Ethereum block header in the **LiteNode** running on NEAR, and make its own independent calculation of the cryptographic proof.
8. If the proof we provided **matches the proof** that the ERC-20 Connector calculates, then it knows those 20 DAI are safely locked away on Ethereum—and that it was me who locked it!—and proceeds to create (mint) 20 new DAI on NEAR and delivers them to my wallet.


When we want to transfer DAI from NEAR back to Ethereum, the process happens in reverse, i.e. rather than locking 20 DAI in NEAR, we destroy them—known as “burning”—and then we provide the “proof” of that burn to the Connector running on Ethereum. Having access to the NEAR blocks in the LiteNode running on Ethereum, it validates our proof, and releases 20 DAI from its vault and sends them to our wallet!

And that, in a nutshell, is how the Rainbow Bridge works! It’s the only Ethereum bridge in crypto that works this way, currently—allowing you to permissionlessly transfer assets between Ethereum, NEAR—and soon, Aurora—**without having to put any trust in third parties**. Very cool!

## Other bits and pieces
Here’s some interesting notes to go along with that overview:

* Since the [NEAR-to-Ethereum](https://learnnear.club/near-ethereum/) Relayer only sends NEAR block headers to the Ethereum LiteNode every 16 hours, there’s a 16 hour delay between steps one and two when moving tokens in that direction. (Remember, this is because Ethereum gas fees make it prohibitively expensive for the Relayer to update the LiteNode on every block.) There are a number of approaches that would allow us to reduce this delay, and the team is actively working on that.
* On NEAR, the LiteNode stores all past Ethereum block headers. In order that storage space doesn’t get out of hand, the LiteNode “prunes” (deletes) blocks older than about two weeks. This means if you start a transfer from Ethereum to NEAR, and go on vacation for three weeks between steps one and two, you won’t be able to complete your transfer, because the Ethereum data stored NEAR necessary to verify your “proof” would have been deleted!
* An interesting property of the NEAR block header design, is that with a single block header, we can compute the history of past blocks for quite a long period. So in theory, the LiteNode on Ethereum only needs a single NEAR block; however, we keep them because the gas costs needed to perform pruning would basically be a waste of resources.
* The team that created the Rainbow Bridge is the same that created Aurora—the NEAR EVM. Since that team has spun-out into its own entity, the Rainbow Bridge will come under its management for operations, maintenance and future evolution.
* The Aurora team are working on “auto-finalization” for the Rainbow Bridge, so that you will no longer have to manually initiate step two of these transfers. This will be very convenient for users (and meaning that you could start your Ethereum to NEAR transfer and then go on vacation!)
* Transfers between Ethereum and Aurora are performed by the Aurora Bridge, which uses the same core technology as the Rainbow Bridge, but augmented to handle the NEAR/Aurora hidden step in the transfers.
* The user interface and experience of the Aurora Bridge is different than Rainbow Bridge, and at some point in the future, these will be harmonized.


Although some technical details have been simplified, you now have a fundamental understanding of how the Rainbow Bridge works!

For a in-depth description of the Rainbow Bridge, you can [read this article](https://near.org/blog/eth-near-rainbow-bridge/), and to keep up with everything related to Aurora, be sure to [follow Aurora on Twitter!](https://twitter.com/auroraisnear)