
8/14/2020 Liqwid Whitepaper (This document is subject to change). Last update: 1/7/2021

Liqwid Finance 
An algorithmic protocol for lending & automated liquidity provision on Cardano














Version 1.1.3
January 2021


Authors 
Dewayne Cameron, Josh Akpan, Tashoma Vilini, Florian Volery, Holger Hartstock
https://www.liqwid.finance/	



Abstract 
In this document we present a non-custodial, decentralized protocol to enable robust money markets with algorithmically optimized interest rates based on current supply & demand of pooled capital, allowing users to seamlessly lend & borrow Cardano native assets. Our protocol establishes a complete peer-to-pool financial ecosystem that utilizes crypto-economics to sufficiently incentivize liquidity providers & liquidators who repay a borrower’s borrow collateral amounts when required, securing the protocol against default risk. We also present upgradeable market parameters configured for each Liqwid market to effectively mitigate market and other protocol risks via decentralized governance mechanisms.

1 Introduction 
The crypto market sector of decentralized finance (DeFi) is in the early stages of disrupting modern global finance’s current operating model by repurposing the broad range of functions within traditional finance and bundling them with verifiably trustless and open protocols via smart contracts and digital assets (tokens) [1]. Unfortunately, the robust credit and identity  verification of traditional financial services (CeFi) has not followed: current DeFi users have little ability to build credit (onchain credit scoring) or a standard identity framework to monetize their generated credit data within protocols. The exact same problem exists for many emerging market CeFi participants trying to access low cost borrows at competitive interest rates [2].  
Interest rates allow anyone to earn on otherwise idle assets, and people without assets (e.g. small businesses, traders) to interact; monetizing the risk of borrow default and the time value of digital assets benefits both participants and enables a secure, positive-yield approach for lenders to put their assets to work [3]. Traditional legacy CeFi money markets service borrowers & lenders from the retail up to institutional levels via debt instruments (Treasury Bills, Eurodollar deposit & futures,  asset-backed securities) and exist to serve five primary functions [4]:
Profitable investments (with low risk)
Finance commerce 
Informs central bank monetary policy (current lending conditions in economy)
Finance industry (secure working capital)
Stimulates self-reliance of commercial banks
For participants borrowing in current DeFi and CeFi options major pain points exists: 
Borrowing choice selection is mostly centralized and does not accurately consider borrowers credit in “cost of money” calculations, this results in predatory payday lending schemes in popular CeFi borrow apps [5] and mispriced cost of money in most DeFi protocols [6].  
With no capability to monetize credit data (or verify “proof of identity”) borrowers are not incentivized to develop quality credit history, this manifests itself in the popular CeFi/DeFi protocols overcharging borrowers with high interest rates Factoring their risk of default (liquidation risk). 
The output of the above points is developers are Factored in the application use case layers they can build on top of.  
Centralized exchanges (e.g. Binance, BitMEX) and Decentralized exchanges (e.g. C.R.E.A.M.Finance, Harvest) [7] enables users to trade digital assets on margin, with “lending markets” built into the exchange protocol’s set of services. These are not fully trustless systems (users must trust that the centralized exchange/Admin key will not get hacked, rug pull scam exit with your assets, or incorrectly close out live positions). In addition, the current DeFi lending protocols have no strategy to account for a borrowing user’s previous borrow repayment history. Today high-quality borrowers are forced to pay the same cost of money as low credit borrowers. 
CeFi (retail up to institutional) and DeFi lending markets allow collateralized and uncollateralized borrows [8] to execute between users directly. Unfortunately, both CeFi and DeFi lending protocols carry tradeoffs that impose significant (opportunity) costs, security risk and result in user experience pain points. In every protocol analyzed lenders have no capability to accurately price a borrower’s default risk (credit metrics) which leads to inefficiently priced interest rates, and a proven governance structure for sufficiently aligning incentives for key protocol users (borrowers, lenders, developers and protocol operators) has not emerged. 

Figure 1. Smart contract enabled Crypto-collateralized lending process flow
In this document we present a non-custodial, decentralized protocol for automated frictionless borrowing of Cardano native tokens without the pain points of existing protocols. Our protocol design uses algorithmically optimized interest rate strategies and crypto economics to build robust money markets for global users. Our protocol facilitates efficient money markets combined with an open-source stack for developers (open API’s, SDK) that powers developers with tools to unlock a web3 world of financial (+credit, data, insurance) applications on Cardano, in doing so stimulating the creation of non-zero-sum wealth.
2 Liqwid protocol 
Liqwid protocol is a decentralized application on the Cardano blockchain that establishes money markets, which are pools of liquidity (Cardano native tokens) with algorithmically calculated interest rates based on current market conditions. Lenders and borrowers of a token connect directly to Liqwid money markets, earning/paying a variable interest rate each block and never needing to negotiate contract terms such as maturity date, interest rate, or required collateral with a peer or counterparty. 
Each market is linked to a unique Cardano native asset (e.g. ADA, LQ), and contains an open-source and publicly-verifiable ledger, with an Index of all transactions and an index containing interest rates since market formation [9].
2.1 Supplying Tokens   
Opposite to the traditional CeFi lending model where a lending participant’s assets are paired and borrowed to a borrowing participant, Liqwid combines the assets of each user into a “liquidity pool” (market).  When a user deposits an asset, it becomes a fungible resource in the market and (in the same transaction) they receive a ratio of  “qTokens”, an interest-bearing asset representing their deposited asset plus interest accrued. qTokens exist as Cardano native assets and thus they may be used in any other Cardano dApp that supports qTokens. This approach enables substantially more liquidity than matched  lending to ensure users can deposit or withdraw their assets at any moment, never needing to wait until borrow maturity. 
Tokens supplied to a market are expressed by a market’s total token balance (“qToken”) which gives  the owner rights to a constantly increasing sum of the underlying native  asset. Over time, as the market accrues interest, which is (by design) a function  of borrowing demand, qTokens translate into an increasing exchange rate (on the  underlying asset to qToken pair) as a function of borrower interest paid. In this way, earning interest is as simple as holding a qToken.  
2.1.1 Target Use Cases 
Participants with long-term investments in ADA and other Cardano native tokens can use a Liqwid market as a one-click positive-yield strategy to generate passive returns on their investment. A user that owns ADA and would like exposure to the USD stablecoin on Cardano can supply their ADA tokens to the Liqwid protocol (including staked ADA), and yield the optimal interest rate (denominated in USD); all with no need for users to sell their ADA, give custody to a third party they must trust, actively manage their tokens, match borrow requests or enter risky default bets with low credit borrowers. 
2.2 Borrowing Assets 
Liqwid allows users to seamlessly borrow Cardano native tokens from markets given they have posted sufficient collateral. Unlike peer-to-peer matched lending protocols, borrowing tokens from Liqwid simply requires a user to select their preferred asset; there are never any contract terms to negotiate, borrow durations, maturity dates, or interest rates based on LTV. Like depositing a token (to receive earn rate), each Liqwid pool has an adjustable interest rate (cost of money), set by supply & demand conditions at the time of borrow origination and automatically updated each transaction, these factors establish Liqwid’s interest rate model for each Liqwid supported asset’s market rates.
2.2.1 Collateral Value
Tokens deposited into protocol smart contracts (expressed as ownership of a qToken) are utilized as collateral to borrow from any Liqwid market. Every market has a collateral factor, on a scale from 0 to 1, to represent the percentage of the underlying token value that can be borrowed from a market. Low-micro market cap tokens have low collateral factors (to mitigate market risk for their illiquidity); their volatility makes them riskier collateral types in the same way liquid, higher market cap tokens have increased collateral factors and function as viable collateral options. The total value of a user’s underlying token balances, multiplied by the collateral factor, equals a user’s borrowing  capacity. 
Participants may borrow an amount equal to, but not exceeding, their borrowing capacity, and users are unable to trigger actions in a Liqwid market (e.g. borrow, swap qToken collateral, or redeem qToken collateral) that would increase the total value of borrowed tokens above their borrowing capacity (this helps effectively mitigate Liqwid’s protocol default risk).   
2.2.2 Risk & Liquidation
If the value of a user account’s outstanding borrows exceeds their borrowing capacity, a portion of their outstanding borrow may be repaid in exchange for the user’s qToken collateral (liquidation call), at  the spot price minus a liquidation discount; this incentivizes arbitrageurs and traders (collateral liquidators) to swiftly repay portions of the borrow value to reduce the user’s borrow exposure levels, simultaneously eliminating the protocol’s default risk across outstanding borrows. 
The percentage of outstanding borrower collateral liquidators can close out, the close factor is the  percent of the borrowed tokens that can be repaid, and ranges from 0 to 1,  such as 33%. The liquidation process step may continuously be called until the user account’s  outstanding borrow value is equal to or less than their borrowing capacity.  
Any Cardano address that owns the borrowed tokens for a given market may trigger the liquidation function, swapping their tokens to receive the borrower’s qToken collateral. As a result of the entire borrow/lend ecosystem contained within the Liqwid protocol, liquidation function calls are a streamlined, trustless process that require zero reliance on centralized systems (e.g. CeFi match lending, order-books).
2.2.3 Target Users 
Enabling users to easily access competitive interest rates from any location Liqwid aims to disrupt incumbent CeFi lending models while returning value to the key protocol user’s (borrowers, lenders, developers, protocol operators and liquidators): 
Borrowers have access to low-cost competitive interest rate borrows & do not need to sell their collateral (instead they can use it to pay their borrow)
Lenders accrue interest at the optimal earn rate; a function of the Pool’s utilization ratio (borrower demand) and volume. 
Developers can build borrowing directly into their Cardano dapp using Liqwid markets or build new dApps using Liqwid open API’s and SDK
Liquidators can earn profits securing Liqwid markets from default risk by repaying borrowers unhealthy borrows (up to close factor). 
Each of the key users highlighted above form the Liqwid ecosystem, the $LQ governance token and LiqwiDAO will establish financial incentives to encourage each of these players to positively contribute to the protocol’s future value.
2.3 Interest Rate Model
Instead of requiring peer-to-peer borrowers or lenders to negotiate over contract terms and interest rates, Liqwid Protocol uses an interest rate model to calculate an interest rate equilibrium, in each market, based on current supply and demand conditions. 
Building on sound macroeconomic theory, interest rates (the “cost” of money) should increase as a direct function of demand; if borrow demand is low, interest rates should be low, and the opposite when borrow demand is high. The utilization ratio U for each Liqwid market a combine’s supply and demand into one variable, Ua: 
Ua = Borrowsa / (Casha + Borrowsa) 
The Governance module includes all functionality required to determine future updates to the demand curve which is represented as a function of utilization Ua. Borrowing interest rates will vary by Liqwid market and will also be updated via governance mechanisms as required in future. 
Borrowing Interest Ratea = 2.3% + Ua * 10% 
The earn rate paid to lenders is baked into the borrow coasts for borrowers: 
Lender Earn Rate = Borrowing Interest Ratea * Ua
2.3.1 Liquidity Incentive Structure 
No protocol can guarantee liquidity thresholds; instead Liqwid depends on the interest rate model to incentivize it with crypto-economics: 
When liquidity is readily available: low interest rates to encourage borrows.
When liquidity is scarce: high interest rates to incentivize borrow repayment and additional deposits
The $LQ emission rate is engineered to bootstrap early liquidity & reward long term liquidity providers. 
3 Protocol Architecture & Design 
The critical functions of Liqwid Protocol operate to establish efficient money markets as a ledger that enables Cardano users to borrow or lend native assets, while calculating accrued interest, a function of the time value of money. Liqwid’s smart contracts (+API’s, PAB’s, data feeds, SDK’s) will all be open-source, publicly accessible and free to use for developers, protocol operators and any other user in line with our core teams founding ethos of complete transparency. 
3.1 qTokens: Cardano native assets
Every Liqwid market is constructed as a smart contract that implements Cardano native assets via the forging policy script. Users account balances are calculated as qToken balances; users can mint(uint amountUnderlying) qTokens by supplying assets to a Liqwid market or redeem(uint amount) qTokens for the underlying native tokens. Spot prices (exchange rate) between qTokens and the underlying asset continuously increase over time, as interest is accrued by borrowers of the asset: 
underlyingBalance +totalBorrowBalancea − reserves a
exchangeRate =				 qTokenSupplya 
If a Liqwid market’s total borrowing balance increases (as a function of demand increasing), the exchange rate between qTokens and the underlying native asset increases. 
Function ABI Description 
Function ABI
Description
mint(uint256 amountUnderlying)
Transfers an underlying native asset into a Liqwid market, updates address sender’s qToken balance.
redeem(uint256 amount) redeemUnderlying(uint256 amountUnderlying)
Transfers an underlying native asset out of a Liqwid market, updates address sender’s qToken balance.
borrow(uint amount)
Reads address sender’s collateral asset value, if enough, transfers the underlying native asset out of a Liqwid market to address sender, and updates address sender’s outstanding borrow balance.
repayBorrow(uint amount) repayBorrowBehalf(address account, uint amount)


Transfers the underlying native asset into the market, updates the user’s borrow balance.
liquidate(address borrower, address collateralAsset, uint closeAmount)


Transfers the underlying native asset into a market, updates the user’s borrow balance, next transfers qToken collateral from the borrower to address sender.




Table 2. Contract application ABI and description of primary qToken smart contract functions

3.2 Interest Rate Strategies 
Liqwid markets are defined by their core functionality, money robots algorithmically optimized for calculating interest rates, which is applied to all borrowers uniformly and dynamically updates to reflect the market’s current supply and demand levels.
Data linked to interest rates for each money market, is stored via an Interest Rate Index, which is auto-updated each time a Liqwid Pool’s interest rate updates, the output of a user minting, redeeming, borrowing, repaying, or liquidating the native (underlying) asset. 
3.2.1 Market Forces 
Every transaction that is executed in a Liqwid market updates the Interest Rate Index for the native asset to accrue the interest since the last Index, using the interest for the time period, defined by r * t, automatically calculated using a per-block interest rate: 
Indexa,n  = Index a,(n−1) * (1 + r * t)
A Liqwid market’s total borrow outstanding is updated to include interest accrued since the last Index:    
totalBorrowBalancea,n  = totalBorrowBalancea,(n−1) * (1 + r * t)

A percentage of markets accrued interest is retained (in a smart contract) as market reserves, determined by a reserveFactor, on a scale from 0 to 1: 
reservesa  = reservesa,(n−1) + totalBorrowBalance a,(n−1) * (r * t * reserveFactor) 
3.2.2 Borrower Forces
A user’s borrow balance, including accrued interest to the underlying native asset can be computed as the ratio of the current rate Index divided by the Index when the borrower’s borrow balance was last checkpointed. 
The balance for each borrower address in the qToken is stored as a forging context (or metadata linked account checkpoint*). A forging context is a Cardano data structure containing a summary of the transaction and the current forging policy which is being run. This forging context (or metadata linked account checkpoint*) contains the balance at the time interest was last applied to that user’s account.
3.3 Borrowing Native Assets
A Liqwid participant who needs a borrow and has deposited collateral may call borrow(uint amount) on their preferred qToken contract. Borrow(uint amount) function call checks the user’s current account value, and if enough collateral is present will update the user’s borrow balance, transfer the underlying native assets to their Cardano address and update the market’s variable interest rates. 
Borrows compound interest in the exact same calculation as balance interest (accrued interest) in the section above. Liqwid market borrowers are entitled to repay an outstanding borrow at any time, by calling repayBorrow(uint amount) or repayBorrowFor(address accountID, uint amount) which repays the outstanding borrow balance in part or full. 
3.4 Liquidation Events
If a Liqwid borrower’s outstanding borrow balance exceeds their total collateral value (borrowing capacity) as a result of falling collateral value (or borrowed assets quickly increasing in value such as the recent Compound oracle exploit) the public liquidation function call liquidate(address target, address collateralAsset, address borrowAsset, uint closeAmount) can be called, which exchanges the liquidator’s native asset for the borrower’s collateral at a given liquidation discount (subsidized amount paid from borrower’s collateral for securing protocol from default risk). 
3.5 Price Feed
Liqwid Price Feeds enable a set of data providers “Reporters” (e.g. exchanges, Dex’s)  to sign price data using a known public key, which “Posters” (any Cardano address) can submit on-chain. These exchange rates are used to determine borrowing capacity and collateral requirements, and for all function calls which require calculating the value equivalent of an account
3.6 Comptroller 
Liqwid protocol will only support specific Cardano native assets (with sufficient address diversity and token liquidity). Every additional market must be created within the Liqwid ecosystem’s governance driven process (Market Formation). Liqwid markets can be created following this governance-approved admin function call, supportMarket(address market, address interest rate model) that allows users to begin engaging directly  with the newly formed market’s native (underlying) asset (no qTokens will exist upon initial Market Formation). For  a user to receive a borrow,  there must be a verifiably accurate spot price from the Price Feed: to use an asset as collateral, there must be a valid spot price & a collateralFactor.  
Each function call is first simulated through Liqwid protocol’s risk management layer, referred to as the Comptroller; this contract validates the borrower’s collateralFactor and current liquidity levels, before enabling a user action to execute.   

3.7 Governance 
The LiqwiDAO structure is being deployed from Day 1 on mainnet to ensure the future voting power within the protocol is effectively distributed amongst the LiqwiDAO members who are helping drive early protocol utility by supplying liquidity. As the Liqwid legion community of developers, liquidity providers and end-users begin engaging with the governance module on mainnet, incentivized voting as well as outcomes-based incentives could introduce a more robust voting system for $LQ holders. 
The $LQ token will be the protocol’s governance token, empowering $LQ holders to vote on updates to the platform. Combining governance mechanisms and incentivizing holders, it will serve to align key stakeholders in the Liqwid ecosystem. Decentralized, automated governance that sufficiently incentivizes users and aims for security, sustainability, and community welfare are critical to a DeFi protocol’s success.
Governance processes include:
The ability to propose/list a new qToken market
The ability to propose/update the interest rate models per market (e.g. update Borrowing Interest Ratea fixed constants)
The ability to introduce new interest rate strategies 
The ability to propose new interest rate models 
The ability to update the oracle pools query Factors (e.g. use the Time-Weighted Average Prices from top 25 exchanges/DEX’s)
The ability to transfer the reserves of a Liqwid market’s qToken after some reserve threshold is reached (e.g. to finance a dev bounty or distribute as additional dividends to LQ holders)
LiqwiDAO controlled by the community (the sole Admin from Day 1); controlled by a community voted multi-sig structure defined in the LiqwiDAO governance module (Rainmaker) 

Governance Distribution
The distribution breakdown is designed to facilitate the most decentralized, community led DeFi protocol and ensure power does not reside in the hands of a few.


Fair Vesting

The Liqwid core team has agreed upon a fair vesting schedule that will gradually release LQ governance tokens to the core team, advisors, and tech partners over the course of the first 146 epochs (5 days in Cardano). The tokens allocated for the Founders, Advisors and Technology partners (25%) are locked in a smart contract that releases the tokens on a per epoch basis for a two-year period. The vesting period begins with the launch of the Yield Farming mechanism (Hydroponica).

Total amount of $LQ tokens: 21,000,000
Percent of $LQ tokens allocated to Founders, Core Team (+ future hires), Advisors, Technology Partners: 25%
Total amount of $LQ tokens vested: 5,250,000
Length of vesting: 146 epochs
Release schedule: 1 epoch
Amount of $LQ tokens released per epoch: 35,958.904 
Percent of $LQ tokens released per epoch: 0.68%
4 Summary 
Liqwid creates robust and securely functioning liquidity pools (markets) for Cardano native assets
Every Liqwid market has interest rates that are determined by the supply and demand of the underlying asset; as borrow demand scales, or when supply is removed, interest rates increase, incentivizing additional users to supply liquidity.
Users can supply tokens to a market to earn interest without giving custody to a central party
Users can borrow a market’s native asset (to use, sell, or re-lend) by using their Liqwid account balance as collateral


Q.E.D.
References 
[1] How DeFi promises to transform financial services. https://www.cityam.com/how-defi-promises-to-transform-financial-services/
[2] How Africa’s growing mobile money market is evolving. https://www.ey.com/en_gl/banking-capital-markets/how-africa-s-growing-mobile-money-market-is-evolving
[3] How interest rates affect markets. https://www.investopedia.com/articles/stocks/09/how-interest-rates-affect-markets.asp
[4] Money Market. https://www.investopedia.com/terms/m/moneymarket.asp
[5] Opay removes oborrow feature. https://techpoint.africa/2020/01/21/opay-removes-oborrow-feature/ 
[6] DeFi and credit. https://cointelegraph.com/news/defi-and-credit-on-the-blockchain-why-borrows-are-better-when-theyre-decentralized
[7] What is Admin Key risk? https://defiwatch.net/admin-key-config-and-opsec/what-is-admin-key-risk 
[8] Aave Whitepaper. https://github.com/aave/aave protocol/blob/master/docs/Aave_Protocol_Whitepaper_v1_0.pdf
[9] Compound Whitepaper https://compound.finance/documents/Compound.Whitepaper.pdf
