# Writing issues

Before using the forms, make sure **Issues** is enabled in the repository's **Settings > General > Features** and publish the `.github/ISSUE_TEMPLATE/` files and this guide to the default branch.

Use the **New issue** button and choose the form that best matches the work:

- **Bug report** for behavior that is broken or unexpected.
- **Feature request** for a capability or improvement.
- **Task** for a defined piece of work that is neither a bug nor a feature proposal.

Before opening an issue, search existing issues for duplicates. Keep each issue focused on one outcome, use a short descriptive title, and include enough detail for someone else to understand or verify the request. Link related issues and avoid posting secrets or personal information.

For bugs, include reproducible steps and the behavior you expected. For feature requests, explain the problem and the desired outcome. For tasks, state the definition of done. Add logs or screenshots only when they help explain the issue.

```mermaid
flowchart TD
    A[Start: prepare repository] --> B[Enable Issues in repository settings]
    B --> C[Publish templates and guide to the default branch]
    C --> D[Notice a problem or idea]
    D --> E[Search existing issues]
    E --> F{Already tracked?}
    F -->|Yes| G[Add details to the existing issue]
    F -->|No| H{What kind of work?}
    H -->|Broken behavior| I[Choose Bug report]
    H -->|New capability or improvement| J[Choose Feature request]
    H -->|Other defined work| K[Choose Task]
    I --> L[Write a clear title and complete required fields]
    J --> L
    K --> L
    L --> M[Check for secrets and add relevant links or evidence]
    M --> N[Submit the issue]
    N --> O[Respond to questions and keep the issue updated]
```
