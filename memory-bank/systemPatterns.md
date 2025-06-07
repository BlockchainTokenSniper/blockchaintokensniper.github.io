# System Patterns: BlockchainTokenSniper (BTS) V3 Website

**Note:** This document describes system patterns relevant to the **BTS V3 Website** as contained in this repository. Patterns related to the bot application's architecture (e.g., `main.js`, `BlockchainLaunchSniper.js`, IPC, detailed user data structures for bot operation, global variables for bot processes) are part of separate, private repositories and are **not applicable here** beyond how they might inform website content (e.g., explaining tiers or features).

## Core Website Architecture

*   **Static Site:** The website is primarily a static HTML, CSS, and JavaScript site.
*   **Templating/Structure:** Likely uses a common header, footer, and navigation structure across pages, potentially managed by a static site generator (like Jekyll, given `just-the-docs` theme) or manually maintained.
    *   The presence of `assets/css/just-the-docs-*.css` and `assets/js/just-the-docs.js` strongly suggests the "Just the Docs" Jekyll theme is in use.
    *   GitHub Pages is likely used for hosting, often paired with Jekyll. The `.github/workflows/static.yml` further supports this, likely for building and deploying the Jekyll site.
*   **Content Management:** Content is directly embedded in HTML files or Markdown files processed by Jekyll.
*   **Configuration (Website Specific):**
    *   Jekyll configuration files (e.g., `_config.yml` - *not currently visible but typical for Jekyll*) would control site-wide settings, navigation, and theme options.
    *   `assets/js/search-data.json` indicates a client-side search functionality, common with "Just the Docs".

## Key Technical Decisions (Website)

*   **Framework/Theme:** Use of "Just the Docs" Jekyll theme for structure, styling, and features like search.
*   **Deployment:** Likely deployed via GitHub Pages, automated by the GitHub Actions workflow in `static.yml`.
*   **Version Control:** Git, hosted on GitHub.

## Component Relationships (Website - High-Level)

```mermaid
graph TD
    subgraph User Facing
        User[User via Browser] --> Website[Live Website on GitHub Pages];
    end

    subgraph Deployment Pipeline
        Repo[GitHub Repository (blockchaintokensniper.github.io)] -- Push/Merge --> GHAction{GitHub Action (static.yml)};
        GHAction -- Builds --> JekyllSite[Jekyll Build Process];
        JekyllSite -- Deploys --> Website;
    end

    subgraph Source Code (This Repository)
        HTMLFiles[HTML Files (index.html, buy/index.html, etc.)] --> JekyllSite;
        MarkdownFiles[Markdown Files (docs/*.md)] --> JekyllSite;
        CSSFiles[CSS (assets/css/*.css)] --> JekyllSite;
        JSFiles[JavaScript (assets/js/*.js)] --> JekyllSite;
        ImageFiles[Images (assets/images/*)] --> JekyllSite;
        JekyllConfig[_config.yml (assumed)] --> JekyllSite;
    end

    style User fill:#DAE8FC,stroke:#6C8EBF,stroke-width:2px
    style Website fill:#D5E8D4,stroke:#82B366,stroke-width:2px
    style Repo fill:#FFF2CC,stroke:#D6B656,stroke-width:2px
    style GHAction fill:#F8CECC,stroke:#B85450,stroke-width:2px
    style JekyllSite fill:#E1D5E7,stroke:#9673A6,stroke-width:2px
```
*Diagram updated to reflect a typical Jekyll and GitHub Pages static website architecture.*

## Critical Implementation Paths (Website)

*   **Content Updates:** Modifying HTML or Markdown files and pushing changes to trigger deployment.
*   **Navigation Changes:** Editing Jekyll configuration or theme includes to update site navigation.
*   **Styling Changes:** Modifying CSS files or theme SASS variables (if applicable).
*   **Deployment Workflow:** Ensuring `static.yml` correctly builds and deploys the site.

*(This document has been refocused to describe the system patterns of the static website contained in this repository, likely built with Jekyll and hosted on GitHub Pages.)*
