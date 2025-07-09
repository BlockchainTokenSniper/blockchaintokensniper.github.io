# BlockchainTokenSniper (BTS) V3 - User Guide

## 1. Introduction

Welcome to the user guide for BlockchainTokenSniper (BTS) V3. This document provides a comprehensive overview of the bot's features, commands, and configuration options.

### 1.1. What is BTS V3?

BTS V3 is a powerful Telegram bot designed for sniping newly launched tokens and automating trades based on signals from Telegram channels. It operates on both EVM-compatible chains (like Ethereum and Binance Smart Chain) and the Solana network.

### 1.2. Core Components

The bot is comprised of three main sniper modules:

*   **BlockchainLaunchSniper (EVM):** Snipe a single token at launch on EVM chains.
*   **BlockchainMultiSniper (EVM):** Automatically monitor Telegram channels for token addresses on EVM chains and execute trades.
*   **BlockchainSolanaSniper (Solana):** Automatically monitor Telegram channels for token addresses on the Solana network and execute trades across multiple DEXs (Jupiter, Raydium, Pump.fun).

---

## 2. Getting Started

Getting started with the BTS V3 bot is a simple process. Here’s a step-by-step guide for new users.

1.  **Start the Bot**: The first step is to send the `/start` command to the bot.

2.  **Language Selection**: You will be prompted to select your preferred language. Currently, only English is fully supported.

3.  **EVM Wallet Setup**: The bot requires an EVM-compatible wallet to function. You will be given two options:
    *   **Import Wallet**: Choose this option to use an existing wallet. You will be asked to provide your wallet's **private key**. The bot will validate the key and save it securely in your local user data file.
    *   **Generate Wallet**: Choose this option to create a new wallet. The bot will generate a new wallet, display your new public address, and save the private key. You can view the private key later in the settings menu.

4.  **Solana Wallet & Telegram API Setup**:
    *   The initial setup only covers the EVM wallet. To use the **SolanaSniper**, you must configure your Solana wallet separately.
    *   Navigate to `/settings` -> `SolanaSniper Settings` -> `Wallet Settings` to import your Solana wallet using its **seed phrase**.
    *   To use the automated MultiSniper or SolanaSniper, you must also add your **Telegram API credentials** in the main settings menu.

5.  **Setup Complete**: Once the initial EVM wallet setup is done, the bot will save your configuration, and the `setupComplete` flag will be set. You can then use the `/start` command again to access the main menu and begin using the bot's features.

---

## 3. User Commands

This section details the commands available to all users.

### 3.1. Core Commands
*   `/start` - Initializes the bot, displays the main menu, and stops any active sniper processes. If you are a new user, it will begin the setup process.
*   `/settings` - Opens the main settings menu.
*   `/help` - Displays the help menu with links to documentation and support.
*   `/commands` - Shows a list of available commands.

### 3.2. Sniper Commands
*   `/launch` - Starts the LaunchSniper for EVM chains. This is used for sniping a specific token at launch.
*   `/multi [y]` - Starts the MultiSniper for EVM chains. This bot automatically trades based on Telegram channel signals. Add `y` to the end (e.g., `/multi y`) to auto-start the bot without seeing the confirmation screen.
*   `/solana [y]` - Starts the SolanaSniper. This bot automatically trades based on Telegram channel signals on the Solana network. Add `y` to the end (e.g., `/solana y`) to auto-start the bot without seeing the confirmation screen.

### 3.3. Trading & Information Commands
*   `/sell` - Lists all currently held tokens in an active MultiSniper or SolanaSniper instance, allowing you to sell them manually.
*   `/sell <ID> [percentage]` - Sells a specific token from the `/sell` list by its ID. You can optionally specify a percentage to sell (e.g., `/sell 1 50` to sell 50% of token ID 1).
*   `/sell all [percentage]` - Sells all tokens currently held by an active sniper.
*   `/sell <ID1>,<ID2> [percentage]` - Sells multiple specific tokens by their IDs.
*   `/sell <token_address> [percentage]` - (Solana Only) Sells a specific Solana token by its contract address.
*   `/list` - Shows your snipe history.
*   `/feesummary` - Displays a summary of your accumulated and paid trading fees.
*   `/refer` - Opens the referral menu to get your referral link and view stats.
*   `/stats` - Shows public statistics for the bot, including total users, transaction volume, etc.
*   `/clearcache` - Deletes the token cache file for your currently active sniper. This can resolve issues where the bot's state is out of sync with the blockchain.
*   `/clear` - Clears the message history in your chat with the bot.

### 3.4. Admin Commands
These commands are restricted to bot administrators.

*   `/adminstats` - Displays detailed statistics about the bot's operation, including user counts, tier breakdowns, fee summaries, and more.
*   `/collectfees` - Manually triggers the global fee collection process for all users.
*   `/markfeesaspaid <userID>` - Manually marks all unpaid fees for a specific user as paid.
*   `/adminsettier <userID>` - Opens a menu to set the Pro Tier status (Voucher, Lifetime, or Free) for a specific user.
*   `/showallsnipes` - Shows a list of all snipes across all users.

---

## 4. Sniper Bot Details

### 4.1. LaunchSniper (EVM)

The LaunchSniper is designed to buy a specific token on EVM-compatible chains as quickly as possible, typically at the moment of launch. It is initiated with the `/launch` command.

#### How it Works

1.  **Initiation**: The user provides the contract address of the token they wish to snipe.
2.  **Anti-Bot Delay**: If configured, the bot can wait for a specific number of blocks to pass before executing the buy. This can help bypass some anti-bot mechanisms that penalize the very first buyers.
3.  **Transaction Building**: The bot automatically determines the correct liquidity path (e.g., WETH -> Your Token) and builds the transaction. It supports both native currency (like ETH or BNB) and token-based buys (e.g., USDC -> Your Token).
4.  **Gas & Slippage**: It uses your configured gas settings (Legacy or EIP-1559) and slippage tolerance to execute the trade.
5.  **Execution**: The transaction is signed locally and sent to the network.
6.  **Confirmation & Monitoring**: Upon a successful buy, the bot logs the transaction, calculates the fees, and immediately starts monitoring the token's price based on your chosen selling strategy (e.g., Basic Autosell, Trailing Stop Loss).

*(Further details on selling and monitoring will be added after analyzing the relevant files.)*

### 4.2. MultiSniper (EVM)

The MultiSniper is an automated trading bot for EVM chains that monitors specified Telegram channels for token contract addresses and executes trades based on your configuration. It is initiated with the `/multi` command.

#### How it Works

1.  **Telegram Connection**: The bot uses your Telegram API credentials (set up in the main settings) to connect as a user client. This allows it to read messages from the channels you specify.
2.  **Channel Monitoring**: It actively listens for new messages in all the channels you have configured for the MultiSniper.
3.  **Address Detection**: It scans message text for valid EVM contract addresses (e.g., `0x...`).
4.  **Filtering**: Each message is passed through a series of filters:
    *   **Whitelist**: The message must contain *all* the keywords you've specified in the channel's whitelist.
    *   **Blacklist**: The message must not contain *any* of the keywords you've specified in the blacklist.
5.  **Deduplication**: The bot keeps track of recently processed tokens to avoid buying the same token multiple times from different messages or channels.
6.  **Liquidity & Safety Checks**: If a token passes the filters, the bot performs two key checks:
    *   It finds the best liquidity pair to trade against (e.g., WETH, USDC).
    *   If enabled, it uses the **Trading Checker** to verify token safety, checking for things like excessive taxes or honeypot code.
7.  **Execution**: If all checks pass, the bot executes the buy using your configured buy amount, gas settings, and slippage.
8.  **Monitoring**: After a successful purchase, the token is added to your portfolio, and the price monitor begins tracking it according to your chosen selling strategy.

*(Further details on buying, selling, and monitoring will be added after analyzing the relevant files.)*

### 4.3. SolanaSniper (Solana)

The SolanaSniper is a powerful, automated trading bot that monitors Telegram channels for Solana-based tokens and executes trades across multiple decentralized exchanges (DEXs). It is initiated with the `/solana` command.

#### How it Works

1.  **Telegram Connection**: The bot uses your Telegram API credentials to connect as a user client, allowing it to read messages from your specified channels.
2.  **Channel Monitoring**: It uses a dual approach for reliability:
    *   **Real-time**: Listens for new message events directly from the Telegram API.
    *   **Polling**: As a fallback, it also polls your configured channels every 2 seconds to ensure no messages are missed.
3.  **Advanced Address Detection**: The bot is designed to find Solana token addresses in various formats:
    *   Plain text Base58 addresses.
    *   `solscan.io/token/...` URLs.
    *   Clickable links in message buttons that point to a Solscan token page.
4.  **Filtering & Deduplication**:
    *   **Whitelist/Blacklist**: Applies your configured keyword filters to the message text.
    *   **Deduplication**: Prevents buying the same token twice if it's posted in multiple channels or messages around the same time.
5.  **Multi-DEX Price Check**: This is a core feature of the SolanaSniper. When a valid token is found, the bot instantly gets quotes from:
    *   **Pump.fun**
    *   **Pumpswap**
    *   **Raydium**
6.  **Best Price Execution**: The bot compares the prices from all available sources and automatically executes the buy on the DEX offering the best price.
7.  **Execution & Monitoring**: The buy is executed using your configured SOL amount, slippage, and priority fee settings. Once purchased, the token is added to your portfolio and the price monitor begins tracking it for a potential sale based on your strategy.

*(Further details on buying, selling, and monitoring will be added after analyzing the relevant files.)*

---

## 5. Configuration Settings

This section details all the configuration options available in the bot's settings menu. These settings allow you to fine-tune the behavior of the sniper bots to match your trading strategy.

### 5.1. General Settings (EVM & Solana)

These settings are found in the main settings menu and apply to all bot types unless specified otherwise.

*   `keepPriceMessageHistory`:
    *   **Description**: If `true`, the bot will not delete previous price update messages, creating a running history in your chat. If `false`, each new price update will replace the last one.
    *   **Default**: `false`
*   `priceChangeAlertThreshold`:
    *   **Description**: The percentage change in price required to trigger a new price update message. For example, a value of `0.1` means a new message will be sent for every 10% change in price.
    *   **Default**: `0.1` (10%)

### 5.2. EVM Sniper Settings

These settings apply to both the **LaunchSniper** and **MultiSniper** on EVM-compatible chains.

#### 5.2.1. General EVM Settings
*   `buyTokens`:
    *   **Description**: Master switch to enable or disable buying.
    *   **Default**: `true`
*   `sellTokens`:
    *   **Description**: Master switch to enable or disable selling.
    *   **Default**: `true`
*   `slippagePercentage`:
    *   **Description**: The maximum allowed slippage for trades, as a percentage.
    *   **Default**: `100`
*   `transactionRevertTime`:
    *   **Description**: The time in seconds after which a pending transaction is considered to have failed.
    *   **Default**: `60`

#### 5.2.2. MultiSniper Specific Settings (EVM)
*   `tradingMode`:
    *   **Description**: Defines the automatic selling strategy.
    *   **Values**: `MANUAL_SELLING`, `BASIC_AUTOSELL`, `TRAILING_STOP_LOSS`, `SELL_AFTER_TIME_DELAY`
    *   **Default**: `MANUAL_SELLING`
*   `totalAllowedSnipes`:
    *   **Description**: The maximum number of snipes the bot will perform before stopping. Set to `-1` for unlimited.
    *   **Default**: `-1`
*   `autoSellPercentage`:
    *   **Description**: The percentage of the token to sell when an auto-sell condition is met.
    *   **Default**: `100`
*   `allowBuyPreviouslyOwnedTokens`:
    *   **Description**: If `true`, the bot can buy a token it has previously owned and sold.
    *   **Default**: `true`
*   `useSingleLiquidityPair`:
    *   **Description**: If `true`, the bot will only trade tokens that have a liquidity pair with the native currency of the chain (e.g., WETH, WBNB).
    *   **Default**: `true`
*   `rugMonitoringEnabled`:
    *   **Description**: If `true`, the bot will attempt to monitor for potential rug pulls.
    *   **Default**: `false`

#### 5.2.3. Trading Strategy Settings (EVM)
*   **Basic Autosell:**
    *   `basicAutosell_AutoSellMultiplier`: The profit multiplier at which to take profit (e.g., `2` for 2x).
    *   `basicAutosell_StopLossMultiplier`: The loss multiplier at which to cut losses (e.g., `0.5` for -50%).
*   **Trailing Stop Loss:**
    *   `trailingStopLoss_MinMultiplier`: The minimum profit multiplier required to activate the trailing stop loss.
    *   `trailingStopLoss_TrailMultiplierAmount`: The percentage the price can drop from its peak before a sell is triggered (e.g., `0.2` for 20%).
    *   `trailingStopLoss_Hardcap`: A fixed profit multiplier at which the token will be sold immediately.
*   **Sell After Time Delay:**
    *   `sellAfterTimeDelay_Blocks`: The number of seconds to wait after a buy before selling.

#### 5.2.4. Transaction & Gas Settings (EVM)
*   `txType`:
    *   **Description**: The type of transaction to use.
    *   **Values**: `Legacy`, `eip1559`
    *   **Default**: `Legacy`
*   **Legacy Gas:**
    *   `legacyTxBuyGasPrice`, `legacyTxApproveGasPrice`, `legacyTxSellGasPrice`: Gas price in Gwei.
    *   `legacyTxBuyGasLimit`, `legacyTxApproveGasLimit`, `legacyTxSellGasLimit`: The gas limit for the transaction.
    *   `legacyAutoGasPriceCalculation`: If `true`, the bot will attempt to calculate the gas price automatically.
*   **EIP-1559 Gas:**
    *   `eip1559BuyMaxPriorityFee`, `eip1559SellMaxPriorityFee`, `eip1559ApproveMaxPriorityFee`: Max priority fee per gas (tip to the validator).
    *   `eip1559BuyMaxBaseFee`, `eip1559SellMaxBaseFee`, `eip1559ApproveMaxBaseFee`: Max base fee you are willing to pay.
    *   `eip1559BuyGasLimit`, `eip1559SellGasLimit`, `eip1559ApproveGasLimit`: The gas limit for the transaction.
    *   `eip1559AutoGasPriceCalculation`: If `true`, the bot will automatically calculate gas prices.
    *   `eip1559AutoGasPricePriority`: The priority level for auto-calculated gas (`Slow`, `Medium`, `Fast`).

#### 5.2.5. Token Safety (Trading Checker)
*   `enableTradingChecker`:
    *   **Description**: If `true`, the bot will perform safety checks on tokens before buying.
    *   **Default**: `true`
*   `tradingChecker_MaxBuyFee`:
    *   **Description**: The maximum allowed buy tax percentage.
    *   **Default**: `20`
*   `tradingChecker_MaxSellFee`:
    *   **Description**: The maximum allowed sell tax percentage.
    *   **Default**: `20`

### 5.3. Solana Sniper Settings

These settings are specific to the **SolanaSniper**.

*   `selectedNetwork`:
    *   **Description**: The Solana network to use.
    *   **Default**: `SOL` (Mainnet)
*   `walletSeedPhrase`:
    *   **Description**: Your Solana wallet seed phrase. **This is stored locally and should be kept secure.**
    *   **Default**: `""`
*   `buyTokens`:
    *   **Description**: Master switch to enable or disable buying.
    *   **Default**: `true`
*   `sellTokens`:
    *   **Description**: Master switch to enable or disable selling.
    *   **Default**: `true`
*   `buyAmount`:
    *   **Description**: The amount of SOL to use for each buy transaction.
    *   **Default**: `0.01`
*   `slippagePercentage`:
    *   **Description**: The maximum allowed slippage for trades.
    *   **Default**: `50`
*   `priorityFee`:
    *   **Description**: The priority fee in SOL to add to transactions to increase their processing speed.
    *   **Default**: `0.00001`
*   `computeUnitLimit`:
    *   **Description**: The maximum number of compute units a transaction can consume.
    *   **Default**: `200000`
*   **Trading Strategy Settings (same as EVM but with `sellAfterTimeDelay_Seconds`)**
    *   `tradingMode`: `MANUAL_SELLING`, `BASIC_AUTOSELL`, `TRAILING_STOP_LOSS`, `SELL_AFTER_TIME_DELAY`
    *   `basicAutosell_AutoSellMultiplier`, `basicAutosell_StopLossMultiplier`
    *   `trailingStopLoss_MinMultiplier`, `trailingStopLoss_TrailMultiplierAmount`, `trailingStopLoss_Hardcap`
    *   `sellAfterTimeDelay_Seconds`: The number of seconds to wait after a buy before selling.

---

## 6. Special Topics

### 6.1. Fee Collection & Referrals

The bot includes a monetization system based on trading fees and a referral program that rewards users for bringing in new members.

#### 6.1.1. Trading Fees

*   **How it Works**: A small percentage of the profit from every successful trade is taken as a fee. This fee is the primary way the bot is monetized.
*   **Fee Calculation**: The fee is calculated on the profit of a trade. If a trade is not profitable, no fee is taken.
*   **Fee Deduction**: Fees are not deducted immediately after each trade. Instead, they are accumulated in a database. The bot runs a process periodically (or when triggered by an admin using `/collectfees`) to deduct the total accumulated fees from the user's wallet.
    *   **For EVM chains**, fees are deducted in the token that was traded (e.g., WETH, USDC).
    *   **For Solana**, all fees are converted to an equivalent SOL value and are deducted as a single, aggregated SOL transaction.
*   **Fee Summary**: Users can check their unpaid and paid fees at any time using the `/feesummary` command.

#### 6.1.2. Referral Program

*   **How it Works**: You can earn a percentage of the revenue generated by users you refer to the bot.
*   **Getting Your Link**: Use the `/refer` command to get your unique referral link.
*   **Your Earnings**:
    *   **Trading Fees**: You earn a percentage of the trading fees collected from users who signed up with your link.
    *   **Tier Purchases**: You earn a percentage of the price when one of your referrals purchases a Pro Tier subscription.
*   **Benefits for Referrals**: New users who sign up with your link receive a discount on their Pro Tier subscription purchase.
*   **Tracking**: The `/refer` menu shows your total number of referrals and a breakdown of your earnings from both trading fees and tier purchases.

### 6.2. Pro Tiers

The bot operates on a freemium model with a **Free Tier** and a **Pro Tier**.

#### 6.2.1. Free Tier Limitations

The Free Tier is fully functional for basic sniping but comes with the following limitations:
*   **Trading Fee**: A 1% fee is applied to the profit of all successful trades.
*   **Configuration Limits**:
    *   Maximum of 1 Telegram channel.
    *   Maximum of 1 liquidity pair.
    *   Whitelist/blacklist filters are disabled.
    *   Token liquidity filters are disabled.
*   **Feature Limits**:
    *   Trailing Stop Loss is disabled.
    *   Auto gas price calculation is disabled.
    *   Cannot use custom RPC nodes.
    *   Can only select the first DEX listed for any given chain.

#### 6.2.2. Pro Tier Benefits

Upgrading to the Pro Tier unlocks the full potential of the bot:
*   **No Trading Fees**: All trading fees are removed.
*   **Unlimited Configuration**: Configure unlimited channels, liquidity pairs, and filters.
*   **All Features Unlocked**: Gain access to advanced features like Trailing Stop Loss, auto gas calculation, custom node support, and all DEX options.
*   **Priority Support**.

#### 6.2.3. How to Upgrade

You can upgrade to the Pro Tier from the main menu. Payments can be made in **BNB** (on Binance Smart Chain) or **SOL**. The following subscription options are available:
*   **Pro Tier (Monthly)**: A recurring monthly subscription. This will attempt to auto-renew each month by deducting the fee from your configured wallet. You can cancel the renewal at any time from the Pro Tier menu, which will convert your subscription to `PRO_EXPIRING`.
*   **Pro Tier (Lifetime)**: A one-time payment for permanent lifetime access to the Pro Tier.
*   **Pro Tier (Voucher)**: A temporary Pro Tier access granted by an admin, which does not auto-renew.
