# Active Context: BlockchainTokenSniper (BTS) V3 Website

**Note:** This repository and context primarily concern the **BTS V3 Website**. Information regarding the BTS V3 bot application's internal workings, development, or specific bug fixes refers to activities in separate, private repositories unless explicitly stated as a website change.

## Current Focus

*   **Website Accuracy**: Ensure all information on the website is accurate and up-to-date.
*   **Cleanup of Old User Guides**: Review if the old, separate user guide files (`BlockchainLaunchSniper/index.html`, etc.) should be removed or redirected, now that the main user guide page links to the individual guides.

## Recent Changes

*   **Security Information Update (Completed 16/07/2025)**:
    *   Corrected the security information in `docs/user-guide/index.html` to state that private keys are stored on BTS V3 servers, not on the user's local machine.

*   **Website Navigation and Content Correction (Completed 16/07/2025)**:
    *   Corrected the "SolanaSniper" link to "BlockchainSolanaSniper" in the navigation bar across all relevant pages.
    *   Corrected the navigation bar on all user guide sub-pages (`BlockchainLaunchSniper`, `BlockchainMultiSniper`, `SolanaMultiSniper`) to ensure the dropdown menu appears correctly and consistently across the entire site.
    *   Updated the navigation bar across all other relevant pages (`index.html`, `404.html`, and all pages in `docs/`) to include a consistent dropdown menu for the User Guides.
    *   Removed outdated Jekyll front matter from `docs/user-guide/index.html`.
    *   Removed outdated Telegram API setup instructions from the `BlockchainMultiSniper` and `SolanaMultiSniper` user guides.

*   **Comprehensive User Guide Overhaul (Completed 07/09/2025)**:
    *   **`docs/user-guide/index.html`**: The main user guide page was updated to serve as a central hub linking to individual, detailed guides for each sniper bot.

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
