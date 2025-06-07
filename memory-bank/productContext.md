# Product Context: BlockchainTokenSniper (BTS) V3

## Problem Solved

*   **Information Overload:** Crypto space is flooded with new tokens and signals across numerous Telegram channels. It's hard for users to track and act quickly.
*   **Speed Advantage:** Manual trading is often too slow to capitalize on initial price pumps of newly launched tokens ("sniping").
*   **Complexity:** Interacting directly with blockchains (swapping, managing gas fees, approving tokens) can be complex for average users.
*   **Profit Opportunity:** Users want to leverage automated tools to profit from rapid price movements in the volatile shitcoin/memecoin market.

## How It Should Work (User Perspective)

*   **Setup:** Users connect their Telegram account, configure wallets, select networks (e.g., BSC, ETH), and potentially choose subscription tiers.
*   **Launch Sniper:** Users provide a contract address, set buy parameters (amount, gas, slippage), and the bot executes the buy as quickly as possible upon liquidity addition or other triggers. It then monitors price and sells based on user-defined profit/loss targets.
*   **Multi Sniper:** Users specify Telegram channels to monitor. The bot automatically detects potential token contract addresses mentioned in messages, performs safety checks (e.g., honeypot, tax), buys the token, monitors price, and sells based on profit/loss targets.
*   **Management:** Users can view active snipes, trade history, profit/loss, and manage settings via the Telegram bot menu.
*   **Notifications:** Users receive Telegram updates on successful buys, sells, errors, and potentially price alerts.

## User Experience Goals

*   **Simplicity:** Abstract away blockchain complexities through an intuitive Telegram interface.
*   **Speed & Reliability:** Execute trades faster than manual methods with high success rates.
*   **Security:** Ensure user funds and data are handled securely.
*   **Profitability:** Provide tools that genuinely help users make profitable trades (within the inherent risks of the market).
*   **Transparency:** Clear reporting on trades, fees, and bot actions.

## Target Audience

*   Crypto traders interested in high-risk, high-reward memecoin/shitcoin trading.
*   Users active in Telegram crypto communities.
*   Individuals looking for automated trading solutions to save time and potentially gain an edge.

*(This is an initial draft based on the provided information and project goals. It will be refined as I analyze the codebase.)*
