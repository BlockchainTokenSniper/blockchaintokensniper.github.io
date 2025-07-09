# Active Context: BlockchainTokenSniper (BTS) V3 Website

**Note:** This repository and context primarily concern the **BTS V3 Website**. Information regarding the BTS V3 bot application's internal workings, development, or specific bug fixes refers to activities in separate, private repositories unless explicitly stated as a website change.

## Current Focus

*   **Comprehensive User Guide Update**:
    *   **Goal**: Overhaul the user guide to be a single, comprehensive document covering all features of the BTS V3 bot.
    *   **Status**: **Completed (07/09/2025)**.
        *   Replaced the content of `docs/user-guide/index.html` with a new, detailed guide provided by the user.
        *   The new guide consolidates information for all snipers (LaunchSniper, MultiSniper, SolanaSniper) and includes detailed sections on commands, settings, and trading modes.
    *   **Next Step**: Review if the old, separate user guide files (`BlockchainLaunchSniper/index.html`, etc.) should be removed or redirected.

## Recent Changes

*   **Comprehensive User Guide Overhaul (Completed 07/09/2025)**:
    *   **`docs/user-guide/index.html`**: Replaced the entire content of the main user guide page with a new, comprehensive guide. This consolidates all previous user guide information into a single, authoritative source.

*   **Website Consistency Update (BlockchainSolanaSniper) (Completed 06/11/2025)**:
    *   **`docs/downloads/index.html`**: Added `BlockchainSolanaSniper` to the list of bots and updated the navigation menu.
    *   **`docs/contact/index.html`**: Updated the navigation menu.
    *   **`docs/migration/index.html`**: Updated the navigation menu.
    *   **`docs/referral-system/index.html`**: Updated the navigation menu.
    *   **`docs/user-guide/BlockchainLaunchSniper/index.html`**: Updated the navigation menu.
    *   **`docs/user-guide/BlockchainMultiSniper/index.html`**: Updated the navigation menu.

*   **Website Content Update (BlockchainSolanaSniper) (Completed 06/11/2025)**:
    *   **`docs/user-guide/SolanaMultiSniper/index.html`**: New file created with comprehensive details on the Solana bot.
    *   **`docs/user-guide/user-guides/index.html`**: Added link to the new Solana user guide in the main list and side navigation.
    *   **`index.html`**: Added BlockchainSolanaSniper to the list of bots and included a new section summarizing its features.
    *   **`docs/supported-blockchains/index.html`**: Added a new section for Solana, mentioning Jupiter API integration.

*   **Website Content Update (Multiple Files) (Completed 06/06/2025)**:
    *   `index.html`: Security notice removed, terminology changed (modules to bots), PRO_VOUCHER removed, nav link removed.
    *   `buy/index.html`: Security notice removed.
    *   `docs/migration/index.html`: Security notice added, V1/V2 migration info added.
    *   `docs/downloads/index.html`: Subscription text updated, terminology changed.

*   **Website Structure Update (Completed 07/06/2025)**:
    *   Removed `docs/smart-contracts/` directory and its contents and all links pointing to it.

## Active Decisions & Considerations

*   **Iterative Website Updates**: Applying website changes in batches per file, or even per section, can be more manageable and less error-prone with current tooling than large, multi-file diffs.
*   **Templating Consistency**: New pages should be created based on the structure of existing pages to maintain a consistent look and feel.
*   **Consolidating Content**: For documentation like user guides, a single, comprehensive page can be more user-friendly and easier to maintain than multiple, fragmented pages.

## Learnings & Project Insights

*   **Tool Limitations with Multiple Changes**: `replace_in_file` can struggle with multiple SEARCH/REPLACE blocks if earlier changes affect the line numbers or exact content expected by later blocks. Sequential, confirmed changes or `write_to_file` are alternatives.
*   **Large-Scale Content Replacement**: For overhauling an entire page's content, `replace_in_file` targeting the `<main>` HTML element is an effective strategy, preserving the site's template structure.

*(This file will be updated frequently as analysis progresses and tasks are undertaken.)*
