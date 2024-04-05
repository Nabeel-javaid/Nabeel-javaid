## Conceptual Overview of Ditto ETH Protocol:

Ditto ETH Protocol is a decentralized finance (DeFi) platform designed to facilitate the creation and trading of synthetic assets pegged to the value of real-world assets. At its core, Ditto ETH employs a unique mechanism that allows users to mint and trade synthetic tokens representing various assets, such as cryptocurrencies, fiat currencies, and commodities, directly on the Ethereum blockchain.

The protocol operates by leveraging a collateralized debt position (CDP) model, where users can lock up collateral in the form of Ether (ETH) to mint synthetic tokens known as dETH, which are pegged 1:1 to the value of Ether. These dETH tokens can then be freely traded on decentralized exchanges (DEXs) or used as collateral to mint additional synthetic assets, providing users with exposure to a wide range of assets without needing to hold the underlying assets themselves.

One of the key features of Ditto ETH is its decentralized price oracle system, which continuously updates the prices of synthetic assets based on real-time market data obtained from external sources such as Chainlink and Uniswap. This ensures that the prices of synthetic assets remain accurate and reflective of their real-world counterparts, thereby maintaining the stability and integrity of the platform.

Moreover, Ditto ETH incorporates various risk management mechanisms, including liquidation protocols and collateralization requirements, to mitigate the risk of insolvency and ensure the safety of user funds. In the event that a user's CDP becomes undercollateralized due to adverse market movements, the protocol may automatically liquidate the CDP to prevent losses and maintain the stability of the platform.

Furthermore, Ditto ETH is governed by a decentralized autonomous organization (DAO), where token holders have voting rights to propose and vote on changes to the protocol, such as adjustments to collateralization ratios or the addition of new synthetic assets. This democratic governance model ensures that the protocol remains adaptable and responsive to the evolving needs of its users.

In summary, Ditto ETH Protocol offers a decentralized and efficient solution for creating and trading synthetic assets on the Ethereum blockchain, providing users with access to a diverse range of assets and investment opportunities while maintaining security, stability, and transparency through its innovative design and governance mechanisms.

[![download.png](https://i.postimg.cc/j2zB0YP3/download.png)](https://postimg.cc/SYxgC5Zc)









## Approach taken in evaluating the DittoETH

Firstly, I thoroughly examined the project overview provided on Code4rena's website to gain a basic understanding of the protocol's purpose and functionality. This overview provided insights into the core features of DittoETH and helped me identify key areas to focus on during the audit.

Next, I delved into the technical aspects of the project by studying the architecture and concepts outlined on the DittoETH website. This included understanding the various facets, libraries, and interfaces used in the protocol, as well as their interactions with each other. Additionally, I reviewed the known issues from a previous audit report by Codehawks to identify potential areas of concern and prioritize my audit accordingly.

During the code review process, I prioritized the examination of critical files based on their importance to the protocol's functionality and security. This involved analyzing contracts such as ShortOrdersFacet.sol, PrimaryLiquidationFacet.sol, BridgeRouterFacet.sol, RedemptionFacet.sol, and ExitShortFacet.sol, which are responsible for crucial operations like creating and matching short orders, handling liquidations, managing bridge credits, and executing redemptions and exit shorts. 

Furthermore, I closely inspected key libraries such as LibSRUtil.sol, LibOrders.sol, LibBridgeRouter.sol, LibShortRecord.sol, LibAsset.sol, LibOracle.sol, and UniswapOracleLibrary.sol, which contain essential functions and utilities used throughout the protocol. 


| Priority | File Name                     | Rationale |
|----------|-------------------------------|-----------|
| 1        | `LibOrders.sol`               | Central to the protocol’s order matching logic; scrutinized for complex vulnerabilities. |
| 2        | `RedemptionFacet.sol`         | Vital for the dUSD to ETH conversion process; critical for maintaining liquidity and user trust. |
| 3        | `BidOrdersFacet.sol`          | Facilitates bid creation and matching; essential for market functionality and engaging user experience. |
| 4        | `ShortOrdersFacet.sol`        | Manages short order logic; crucial for leveraging features and overall protocol stability. |
| 5        | `PrimaryLiquidationFacet.sol` | Governs liquidation processes; imperative for market health and mitigating insolvency risks. |
| 6        | `LibOracle.sol`               | Price feed accuracy impacts all operations; evaluated for timeliness and reliability. |
| 7        | `BridgeRouterFacet.sol`       | Manages cross-protocol interactions; essential for LST deposit/withdrawal processes. |
| 8        | `ExitShortFacet.sol`          | Enables users to exit shorts; paramount for ensuring user confidence and liquidity. |
| 9        | `LibSRUtil.sol`               | Supplements short record functionalities; scrutinized for data accuracy and efficiency. |
| 10       | `LibBridgeRouter.sol`         | Underpins bridge operations; essential for managing bridge credits and facilitating withdrawals. |
| 11       | `LibBytes.sol`                | Utilized for handling proposal data; critical for ensuring data integrity and protocol operations. |
| 12       | `UniswapOracleLibrary.sol`    | Provides fallback TWAP price feeds; essential for oracle reliability and price accuracy. |

By conducting a systematic and thorough review of the codebase, I aimed to identify any potential vulnerabilities, logic errors, or security risks that could pose threats to the integrity and functionality of the DittoETH protocol.



## Core Functionality:
   Core functionality of the DittoETH protocol revolves around the following key components, listed in order of importance:

   1. **ShortOrdersFacet**: This facet is crucial as it handles the creation and matching of short orders within the protocol. It ensures that short orders are properly created, validated, and executed, playing a central role in the shorting mechanism of DittoETH.

   2. **PrimaryLiquidationFacet**: Responsible for facilitating the liquidation process using on-chain observations, this facet is vital for maintaining the stability of the protocol by liquidating undercollateralized positions in a timely manner. It ensures that liquidations occur according to protocol parameters and safeguards against potential insolvency events.

   3. **RedemptionFacet**: This facet enables users to swap dUSD for ETH, akin to the functionality provided by Liquity. It is essential for managing the redemption mechanism within DittoETH and ensures the efficient exchange of assets between users.

   4. **BridgeRouterFacet**: Handling the depositing and withdrawing of LSTs (Liquidity Short Tokens), this facet plays a crucial role in managing bridge credits and facilitating arbitrage opportunities between different collateral types within the protocol.

   5. **ExitShortFacet**: Facilitating the process for a shorter to exit their short position, this facet ensures that users can efficiently unwind their positions when necessary. It is essential for maintaining liquidity and stability within the protocol.

   6. **LibOrders**: This library provides essential functions for managing orders and order matching within DittoETH. It is integral to the functioning of the protocol's trading system and ensures that orders are executed accurately and efficiently.

   7. **LibOracle**: Responsible for fetching price data from external oracles such as Chainlink and Uniswap, this library is critical for determining asset prices within the protocol. It ensures that accurate and up-to-date price information is used for various operations, including liquidations and redemptions.

   8. **LibSRUtil**: Providing miscellaneous functions related to ShortRecords, this library includes logic for calculating recovery collateral ratios, enforcing minimum short ERC amounts, and managing the transfer of short records between users. It plays a supporting role in ensuring the integrity and efficiency of DittoETH's shorting mechanism.

   These core functionalities collectively enable DittoETH to operate as a decentralized synthetic asset protocol, allowing users to engage in shorting, liquidation, redemption, and arbitrage activities within a secure and efficient ecosystem.



## Architecture:

**Smart Contract: BidOrdersFacet**

**Breakdown of Functions:**
- `placeBid(uint256, uint256, address)`: Places a bid order with specified parameters.
- `removeBid(uint256)`: Removes a bid order based on its ID.
- `updateBid(uint256, uint256, uint256)`: Updates an existing bid order with new parameters.
- `bidOrder(uint256)`: Retrieves information about a specific bid order.
- `bidExists(uint256)`: Checks if a bid order exists.

**Key Functions:**
- `placeBid(uint256, uint256, address)`: Allows users to place new bid orders in the system.
- `removeBid(uint256)`: Enables users to remove their existing bid orders.
- `updateBid(uint256, uint256, uint256)`: Allows users to update the parameters of their existing bid orders.

**Smart Contract: ShortOrdersFacet**

**Breakdown of Functions:**
- `createShort(uint256, uint256, uint256, address)`: Creates a new short order with specified parameters.
- `cancelShort(uint256)`: Cancels a short order based on its ID.
- `updateShort(uint256, uint256, uint256)`: Updates an existing short order with new parameters.
- `shortOrder(uint256)`: Retrieves information about a specific short order.
- `shortExists(uint256)`: Checks if a short order exists.

**Key Functions:**
- `createShort(uint256, uint256, uint256, address)`: Allows users to create new short orders in the system.
- `cancelShort(uint256)`: Enables users to cancel their existing short orders.
- `updateShort(uint256, uint256, uint256)`: Allows users to update the parameters of their existing short orders.

**Smart Contract: PrimaryLiquidationFacet**

**Breakdown of Functions:**
- `liquidate(address, address)`: Initiates the liquidation process for a specific shorter's position.
- `liquidateFromTop(uint256)`: Initiates liquidation starting from the top of the liquidation queue.
- `disputeLiquidation(uint256)`: Disputes a liquidation proposal initiated by another user.
- `claimLiquidation(uint256)`: Claims rewards for participating in the liquidation process.
- `liquidationQueue(uint256)`: Retrieves information about a liquidation proposal in the queue.
- `liquidationStatus(address)`: Retrieves the current status of a shorter's position in the liquidation process.

**Key Functions:**
- `liquidate(address, address)`: Initiates the liquidation process for a specific shorter's position, triggering the liquidation queue mechanism.
- `disputeLiquidation(uint256)`: Allows users to dispute a liquidation proposal initiated by another user if they believe it is incorrect or unfair.
- `claimLiquidation(uint256)`: Enables users to claim rewards for participating in the liquidation process, incentivizing their involvement in maintaining the stability of the protocol.



**Smart Contract: BridgeRouterFacet**

**Breakdown of Functions:**
- `deposit()`: Allows users to deposit assets into the protocol.
- `withdraw()`: Allows users to withdraw assets from the protocol.
- `transferBridgeCredit()`: Transfers bridge credit between users.
- `exitShort()`: Handles the exit process for a shorter, including transferring their remaining collateral and debt.
- `redeemCredit()`: Allows users to redeem their bridge credit for the underlying asset.

**Key Functions:**
- `deposit()`: Facilitates the deposit of assets into the protocol, enabling users to participate in shorting or other activities.
- `withdraw()`: Enables users to withdraw assets from the protocol, providing liquidity and flexibility for their holdings.
- `transferBridgeCredit()`: Manages the transfer of bridge credit between users, facilitating efficient asset transfers within the protocol.
- `exitShort()`: Handles the process for a shorter to exit their short position, ensuring proper transfer of remaining collateral and debt.
- `redeemCredit()`: Allows users to redeem their bridge credit for the underlying asset, providing liquidity and flexibility for their holdings.


**Smart Contract: ExitShortFacet**

**Breakdown of Functions:**
- `exitShort()`: Initiates the exit process for a shorter, including transferring their remaining collateral and debt.
- `cancelShort()`: Cancels a short order, releasing locked collateral.
- `combineShorts()`: Combines multiple short orders of the same asset and shorter into one order.

**Key Functions:**
- `exitShort()`: Manages the exit process for a shorter, ensuring the proper transfer of remaining collateral and debt upon exit.
- `cancelShort()`: Handles the cancellation of a short order, releasing locked collateral and preventing execution.
- `combineShorts()`: Facilitates the combination of multiple short orders of the same asset and shorter into one order, streamlining the shorting process and optimizing capital efficiency.


**Smart Contract: RedemptionFacet**

**Breakdown of Functions:**
- `proposeRedemption()`: Initiates a redemption proposal, allowing users to swap dUSD for ETH.
- `disburseCollateral()`: Distributes collateral to users participating in redemptions.
- `claimRemainingCollateral()`: Allows users to claim remaining collateral after a redemption proposal has been finalized.
- `finalizeRedemption()`: Finalizes a redemption proposal, executing the swap of dUSD for ETH and distributing rewards.

**Key Functions:**
- `proposeRedemption()`: Starts the redemption process by creating a proposal for users to swap dUSD for ETH, ensuring proper execution and fairness in the redemption mechanism.
- `disburseCollateral()`: Handles the distribution of collateral to users participating in redemption proposals, ensuring accurate allocation based on user contributions.
- `claimRemainingCollateral()`: Enables users to claim any remaining collateral after a redemption proposal has been executed, ensuring transparency and fairness in collateral distribution.
- `finalizeRedemption()`: Finalizes a redemption proposal by executing the swap of dUSD for ETH and distributing rewards to participants, ensuring the smooth operation of the redemption mechanism and incentivizing user participation.


**Smart Contract: LibBridgeRouter**

**Breakdown of Functions:**
- `deposit()`: Allows users to deposit assets into the bridge router.
- `withdraw()`: Allows users to withdraw assets from the bridge router.
- `getBridgeCredit()`: Retrieves the amount of bridge credit available for a specific user.
- `transferBridgeCredit()`: Transfers bridge credit from one user to another.

**Key Functions:**
- `deposit()`: Facilitates the deposit of assets into the bridge router, enabling users to move assets between the DittoETH protocol and external systems.
- `withdraw()`: Manages the withdrawal of assets from the bridge router, allowing users to retrieve their assets from the DittoETH protocol.
- `getBridgeCredit()`: Retrieves the amount of bridge credit available for a specific user, providing transparency and visibility into users' bridge credit balances.
- `transferBridgeCredit()`: Facilitates the transfer of bridge credit from one user to another, enabling users to transfer their bridge credit balances to other participants in the protocol.


**Smart Contract: LibOracle.sol**

**Breakdown of Functions:**
- `getChainlinkOraclePrice()`: Retrieves the latest price from the Chainlink oracle.
- `getUniswapTWAP()`: Calculates the time-weighted average price (TWAP) from Uniswap.
- `getPrice()`: Fetches the price from the Chainlink oracle and falls back to Uniswap TWAP if the Chainlink oracle is unavailable or outdated.

**Key Functions:**
- `getChainlinkOraclePrice()`: Retrieves the latest price from the Chainlink oracle, providing real-time price data for assets integrated with the protocol.
- `getUniswapTWAP()`: Calculates the time-weighted average price (TWAP) from Uniswap, offering an alternative price oracle mechanism in case the Chainlink oracle is unavailable or outdated.
- `getPrice()`: Fetches the price from the Chainlink oracle and falls back to Uniswap TWAP if the Chainlink oracle is unavailable or outdated, ensuring reliable and up-to-date price data for protocol operations.

## ShortOrdersFacet

The `ShortOrdersFacet` is a crucial component of the DittoETH protocol, responsible for handling the creation and matching of short orders. Let's delve into its implementation and flow:

1. **createShort Function**: This function allows users to create a new short order for a specific asset. It takes parameters such as the asset address, desired collateral amount, and ERC20 debt amount. Upon invocation, the function performs validations to ensure that the provided collateral meets the minimum requirements and that the user has sufficient ERC20 tokens to cover the debt. If the validations pass, the function creates a new short order and stores it in the protocol's data structures.

2. **matchShort Function**: When a short order is created, it waits to be matched with available bids. The `matchShort` function handles this matching process. It iterates through the list of existing bids, searching for a suitable match based on predefined criteria such as price and quantity. Once a matching bid is found, the function executes the trade by transferring collateral from the bidder to the shorter and ERC20 debt tokens from the shorter to the bidder. This process ensures that short orders are efficiently executed according to market conditions.

3. **cancelShort Function**: In case a shorter wishes to cancel their short order, they can do so using the `cancelShort` function. This function performs necessary validations to ensure that the cancellation request is legitimate and that the order exists. If the validations pass, the function refunds any collateral associated with the short order to the user's account, effectively canceling the order.

The logic implemented in the `ShortOrdersFacet` ensures the smooth operation of the shorting mechanism within the DittoETH protocol. It provides users with the ability to create, match, and cancel short orders in a secure and efficient manner, contributing to the overall functionality and stability of the platform.

## Bridging Fees Calculation
Bridging fees calculation involves determining the fees incurred when depositing or withdrawing assets through the bridge in the DittoETH protocol. The fees are typically calculated based on factors such as the amount being transacted, current network conditions, and any additional parameters set by the protocol.

The process of bridging fees calculation in DittoETH can be outlined as follows:

1. **Deposit Fees Calculation**: When a user deposits assets into the bridge, the protocol calculates the deposit fee based on the deposited amount. This fee may vary depending on the type of asset being deposited and any applicable fee structures defined by the protocol.

2. **Withdrawal Fees Calculation**: Similarly, when a user withdraws assets from the bridge, the protocol calculates the withdrawal fee based on the withdrawn amount. The fee calculation may take into account factors such as network congestion and withdrawal limits set by the protocol.

3. **Dynamic Fee Adjustment**: The protocol may adjust bridging fees dynamically based on current network conditions, such as gas prices and transaction volume. This ensures that fees remain reasonable and competitive, even during periods of high network congestion.

4. **Fee Distribution**: Once the fees are calculated, they may be distributed to various parties involved in the bridging process, such as liquidity providers, governance token holders, or the protocol treasury. The distribution mechanism is typically determined by the protocol's governance parameters and may vary depending on the specific use case.

## Calculations involved in Ditto

In DittoETH, several calculations are involved in various aspects of the protocol to ensure its functionality and stability:

1. **Price Calculation**: Price calculations are crucial for determining the value of assets, which is essential for trading, liquidations, and redemptions. The protocol relies on oracles such as Chainlink and Uniswap to fetch price data, which is then used to calculate asset prices based on predefined formulas or algorithms.

2. **Collateral Ratio Calculation**: The collateral ratio is a key metric used to determine the health of short positions and assess their risk of liquidation. It is calculated by dividing the value of collateral assets by the value of the debt (e.g., dETH) held in a short position. If the collateral ratio falls below a certain threshold, the position may be at risk of liquidation.

3. **Yield Calculation**: Yield calculations are used to determine the interest or yield generated by various assets held within the protocol. This includes yields generated by short positions, collateral assets, and other protocol mechanisms. Yield calculations may be based on factors such as interest rates, utilization rates, and market conditions.

4. **Bridge Fees Calculation**: When assets are transferred across different blockchains using the bridge mechanism, fees may be incurred. These fees are calculated based on factors such as transaction size, network congestion, and protocol-specific parameters. The protocol may use predefined fee structures or dynamic algorithms to calculate bridge fees accurately.

5. **Redemption Fee Calculation**: When users redeem dUSD for ETH or other collateral assets, a redemption fee may be applied. The calculation of redemption fees typically involves predefined fee rates or formulas, which may be based on factors such as redemption size, protocol parameters, and governance decisions.

6. **Liquidation Penalty Calculation**: In the event of liquidations, a penalty may be applied to undercollateralized positions to cover potential losses incurred by the protocol. The calculation of liquidation penalties involves determining the amount of the penalty based on factors such as the severity of the undercollateralization and the protocol's risk parameters.

Overall, these calculations play a crucial role in the functioning of DittoETH, ensuring accurate pricing, risk assessment, and fee management within the protocol. They are implemented using predefined formulas, algorithms, and protocol parameters to maintain the integrity and efficiency of the system.

## Comprehensive diagram 
<br/>

[![Screenshot-from-2024-04-06-00-48-54.png](https://i.postimg.cc/Wz7tnnsD/Screenshot-from-2024-04-06-00-48-54.png)](https://postimg.cc/H8VpWbcH)

## Systematic Risks:
The DittoETH protocol is subject to several systematic risks that could potentially impact its operation and stability:

1. **Smart Contract Interactions**: DittoETH interacts with various external smart contracts and protocols for functions such as trading, borrowing, and lending. Integration with these contracts introduces risks such as reentrancy attacks, front-running, and unexpected interactions.


## Technical Risks
Smart Contract Vulnerabilities: Bugs or logical errors in the smart contracts can lead to loss of funds, unauthorized access, or unintended behavior. Given the complexity of contracts and incentive the attack surface is significant.

Scalability Concerns: As transaction volumes grow, the platform must scale without compromising performance or security

## Integration risks 
Integartion Risks in DittoETH primarily stem from the interaction between the protocol and external systems, including oracles, bridges.

1. **Oracle Dependency**: DittoETH relies on external oracles such as Chainlink and Uniswap for fetching price data. Integration with these oracles introduces risks such as oracle manipulation attacks, inaccurate pricing data, and dependency on third-party infrastructure. Any vulnerabilities or manipulations in the oracle systems could lead to incorrect pricing information being used within the protocol, impacting trading, liquidations, and redemptions.

2. **Bridge Integration**: The protocol utilizes bridges to facilitate the transfer of assets between different blockchains. Integration with bridges introduces risks such as bridge failures, network congestion, and smart contract vulnerabilities. Issues with bridge integration could result in delays, loss of funds, or other disruptions to the protocol's operations.

## New learnings and insights from this audit:

Through the audit of DittoETH, I gained several new learnings and insights into decentralized finance protocols and smart contract development practices. Some of the key takeaways include:

1. **Oracle Integration**: I gained a deeper understanding of how DeFi protocols integrate with external oracles to fetch price data for asset valuation and trading. This audit highlighted the importance of using reliable and decentralized oracles to ensure the accuracy and integrity of price information within the protocol.

2. **Bridge Mechanisms**: Exploring DittoETH's bridge mechanisms provided insights into how protocols facilitate the transfer of assets between different blockchain networks. Understanding bridge integrations and associated risks is crucial for assessing the interoperability and resilience of DeFi protocols.

3. **Smart Contract Design Patterns**: Reviewing the codebase of DittoETH exposed me to various smart contract design patterns and best practices for developing secure and efficient DeFi protocols. Analyzing the implementation of features such as short orders, liquidations, and redemptions helped me identify common patterns and considerations for smart contract development.


Overall, the audit of DittoETH provided valuable insights into the complexities and considerations involved in developing and auditing decentralized finance protocols. These learnings will inform my future work in assessing and improving the security, reliability, and usability of DeFi applications.

