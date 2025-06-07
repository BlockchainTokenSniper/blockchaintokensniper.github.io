# Tech Context: BlockchainTokenSniper (BTS) V3 Website

**Note:** This document describes the technical context relevant to the **BTS V3 Website** as contained in this repository. Technologies, dependencies, and configurations related to the bot application itself (e.g., Node.js specifics for the bot, `ethers`/`web3` usage for blockchain interaction, Telegram API libraries for bot communication, SQLite for bot databases, detailed `.env` variables for bot operation) are part of separate, private repositories and are **not applicable here** except for how they might be generally described on the website.

## Core Website Technologies

*   **Primary Languages:** HTML, CSS, JavaScript (for client-side interactivity).
*   **Static Site Generator:** **Jekyll** (inferred from "Just the Docs" theme usage and typical GitHub Pages setups).
    *   The presence of `assets/css/just-the-docs-*.css`, `assets/js/just-the-docs.js`, and `assets/js/search-data.json` strongly indicates the "Just the Docs" Jekyll theme.
*   **Templating Language (within Jekyll):** Liquid.
*   **Content Format:** HTML files and Markdown (`.md`) files (processed by Jekyll).
*   **Styling:** CSS, potentially SASS/SCSS if the theme uses it (Jekyll supports SASS compilation).
*   **Client-Side JavaScript:**
    *   `assets/js/just-the-docs.js`: Theme-specific JavaScript for features like navigation, search, etc.
    *   Potentially other custom JavaScript for minor website enhancements if any.
*   **Package Manager (for development environment, if any):** Not directly evident for a simple static site, but if Jekyll or its dependencies were managed locally, RubyGems (for Jekyll) and potentially npm/Yarn (for JS/CSS build tools if used) could be involved. However, for GitHub Pages deployment, GitHub handles the Jekyll build.

## Development & Setup (Website)

*   **Version Control:** Git.
*   **Hosting:** GitHub Pages (inferred from repository name `blockchaintokensniper.github.io` and common practice).
*   **Deployment:** Automated via GitHub Actions, as defined in `.github/workflows/static.yml`. This workflow likely:
    1.  Checks out the code.
    2.  Sets up Ruby and Jekyll.
    3.  Installs Jekyll dependencies (gems).
    4.  Builds the Jekyll site (HTML, CSS, JS output).
    5.  Deploys the built site to the `gh-pages` branch or directly serves it.
*   **Configuration Files (Website - Jekyll):**
    *   `_config.yml` (standard Jekyll configuration file - *assumed to exist but not currently visible*): Controls site-wide settings, theme, navigation, collections, etc.
    *   Theme-specific configuration files might also be present.
*   **Dependencies (Website - visible):**
    *   The "Just the Docs" theme and its assets.
    *   No `package.json` or `Gemfile` is visible at the root, suggesting dependencies are either vendored with the theme or managed by GitHub Pages' Jekyll build environment.

## Technical Constraints & Considerations (Website)

*   **Static Nature:** The site is static, meaning dynamic server-side processing (like user logins directly on the site, or database interactions beyond what a static site generator pre-processes) is not natively supported. Any such features would rely on external services or client-side JavaScript interacting with APIs.
*   **Jekyll/GitHub Pages Limitations:** Subject to the capabilities and limitations of the Jekyll build environment provided by GitHub Pages (e.g., supported Jekyll version, allowed plugins).
*   **Security (Website):**
    *   Standard web security practices for static sites apply (e.g., HTTPS, ensuring linked external resources are secure).
    *   No user data is stored or processed directly by this website beyond analytics or basic form submissions if any (which would typically go to a third-party service).
    *   The primary security concern is ensuring the integrity of the codebase and the deployment pipeline.

*(This document has been refocused to describe the technical context of the static website contained in this repository, likely built with Jekyll and hosted on GitHub Pages.)*
