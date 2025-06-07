# Active Context: BlockchainTokenSniper (BTS) V3

# Active Context: BlockchainTokenSniper (BTS) V3 Website

**Note:** This repository and context primarily concern the **BTS V3 Website**. Information regarding the BTS V3 bot application's internal workings, development, or specific bug fixes (e.g., `UnableToPopulateNonceError`, `process_fees.js`) refers to activities in separate, private repositories unless explicitly stated as a website change.

## Current Focus

*   **Finalize Website Updates Based on User Feedback**:
    *   **Goal**: Implement all requested changes across `index.html`, `buy/index.html`, `docs/migration/index.html`, and `docs/downloads/index.html`.
    *   **Status**:
        *   **Implemented (06/06/2025, ~7:39pm)**:
            *   **`index.html`**:
                *   Security notice removed (moved to `docs/migration/index.html`).
                *   Changed "sniping modules" & "Module" to "sniping bots" & "Bot" in relevant text and headings.
                *   Removed "PRO_VOUCHER" from Pro Tier description.
                *   Removed "Smart contracts" link from the main navigation menu.
            *   **`buy/index.html`**:
                *   Security notice removed (moved to `docs/migration/index.html`).
            *   **`docs/migration/index.html`**:
                *   Added the "Important Security Notice" section.
                *   Added a new section: "Migrating from BTS V1/V2 to V3?", including details on contacting support and potential complimentary Pro access for previous users.
            *   **`docs/downloads/index.html`**:
                *   Updated the list item about tiers to: "Exploring tier options: A Free Tier is available, and subscribing to a Pro Tier unlocks the full range of advanced features."
                *   Changed "module" to "bot" in list items for consistency.
*   **Previous Focus (Bot Application - External Repo)**:
    *   Fix `UnableToPopulateNonceError` - `modules_main/process_fees.js` (Implemented 06/06/2025, ~7:16pm): Corrected argument passing in `deductFees`. This was a bot application fix, not a website change.
*   (Other previous focuses as documented before, contextualized as website or external bot changes)
    *   **Next Step**:
        1.  **User Review of All Website Changes**: User to review all modified website pages (`index.html`, `buy/index.html`, `docs/migration/index.html`, `docs/downloads/index.html`) for accuracy, clarity, and completeness.
        2.  **User Testing of Fee System (Bot Application - External Repo)**: (Ongoing from previous step) User to test fee deduction in the bot application.
        3.  (Other general testing steps as previously listed in `progress.md`, contextualized)

## Recent Changes

*   **Website Content Update (Multiple Files) (Completed)**:
    *   `index.html`: Security notice removed, terminology changed (modules to bots), PRO_VOUCHER removed, nav link removed.
    *   `buy/index.html`: Security notice removed.
    *   `docs/migration/index.html`: Security notice added, V1/V2 migration info added.
    *   `docs/downloads/index.html`: Subscription text updated, terminology changed.
*   **Bot Application Fix (External Repo) (Completed)**: Corrected argument passing in `deductFees` (`modules_main/process_fees.js`).
*   **Website Structure Update (Completed 07/06/2025)**:
    *   Removed `docs/smart-contracts/` directory and its contents.
    *   Removed link to `docs/smart-contracts/` from `404.html`.
*   (Other previous changes as documented in `progress.md`, contextualized)


## Active Decisions & Considerations

*   **Iterative Website Updates**: Applying website changes in batches per file, or even per section, can be more manageable and less error-prone with current tooling than large, multi-file diffs.
*   (Other previous decisions retained)

## Learnings & Project Insights

*   **Tool Limitations with Multiple Changes**: `replace_in_file` can struggle with multiple SEARCH/REPLACE blocks if earlier changes affect the line numbers or exact content expected by later blocks. Sequential, confirmed changes or `write_to_file` are alternatives.
*   (Other previous learnings retained)

*(This file will be updated frequently as analysis progresses and tasks are undertaken.)*
