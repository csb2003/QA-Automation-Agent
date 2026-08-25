```markdown
# QA Automation Agent (`qa-automation-agent`)

An autonomous QA automation agent and skill specification for Playwright test repositories. It transforms business workflow descriptions into resilient, maintainable, Page Object Model (POM)-based Playwright tests using live UAT exploration and Playwright MCP.

---

## Architecture & Concept

In standard enterprise environments, application source code (Angular/React/Vue frontend repos) is often separated from the test automation repository. 

This agent bridges that gap by using:
* **The Automation Repository** (`playwright.config.ts`, `pages/`, `tests/`, fixtures) for code structure, conventions, and reusable flows.
* **Playwright MCP + Live UAT** as the single source of truth for DOM structure, accessibility trees, and UI behavior.


```

```
   QA Member (Business Intent & Rules)
                   │
                   ▼
        [ QA Automation Agent ]
         │                  │
         ▼                  ▼
[Automation Repo]   [Playwright MCP]
- POMs              - Live UAT Browser
- Fixtures          - Accessibility Trees
- Existing Flows    - Dynamic State / Forms
         │                  │
         └─────────┬────────┘
                   ▼
        [ Reliable Automated Test ]

```

```

---

## Key Capabilities

* **Autonomous UI Discovery:** Inspects accessibility snapshots (`ariaSnapshot()`), labels, and `formcontrolname` attributes in real time rather than guessing selectors.
* **Component-Aware Interactions:** Built-in heuristics for Angular Material, dynamic dropdowns (`mat-select`), custom radio/checkbox controls, and asynchronous file uploads.
* **Business-Driven POM Design:** Creates high-level domain methods (`fillProgramDetails()`, `selectDecision()`) instead of raw mechanical actions (`clickButton()`).
* **Self-Healing & Verification:** Executes the generated test locally, analyzes failure traces, repairs selectors or timing issues, and re-executes until business assertions pass.
* **Defect Isolation:** Distinguishes between automation defects (flaky selector, improper wait) and true application defects (server error, broken validation).

---

## Repository Structure

Designed to fit standard Playwright project layouts:

```text
.
├── pages/                  # Page Object Models
├── tests/
│   ├── flows/              # Reusable multi-step end-to-end flows
│   └── specs/              # Test specifications
├── fixtures/               # Test fixtures and auth helpers
├── playwright.config.ts    # Config containing UAT baseURL
└── qa-automation-agent.md  # Agent skill instructions

```

---

## Setup & Usage

### 1. Installation

Add the skill specification file (`qa-automation-agent.md`) to your project root or your AI agent's configuration directory (e.g., Cursor Rules `.cursorrules`, Windsurf, or Claude Desktop MCP settings).

### 2. Configure Playwright MCP

Ensure Playwright MCP is enabled in your toolchain to allow the agent to launch and inspect the live UAT instance.

### 3. Example Prompting

Pass high-level business requirements directly to the agent:

```text
Automate the user creation and role assignment workflow:
- Role: Super Admin
- Input: Valid enterprise user payload
- Action: Fill profile details, assign "Billing Manager" role, and submit
- Verification: User appears with status "Active" in the User Management grid

```

---

## Agent Lifecycle

1. **Intake & Clarification:** Validates test data, user roles, prerequisites, and destructive action safety.
2. **Repository Discovery:** Inspects existing POMs, fixtures, and authentication helpers for reuse.
3. **Live UAT Exploration:** Inspects DOM/A11y trees via Playwright MCP to find stable locators.
4. **Implementation:** Generates or extends POMs and test specs following existing coding standards.
5. **Execution & Diagnosis:** Runs `npx playwright test`, inspects errors, fixes any automation bugs, and re-runs.
6. **Reporting:** Outputs verified results, modified files, and locator decisions.

---

## Author & License

* **Repository:** [csb2003](https://github.com/csb2003)
* **License:** MIT

```

```
