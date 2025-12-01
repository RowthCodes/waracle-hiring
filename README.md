# testautomation-playwright-mvp

A minimal, opinionated test automation MVP combining Playwright (TypeScript) and example C# test projects. This repository provides a starting point for end-to-end browser testing with Playwright, plus a .NET solution for teams who prefer C#.

- Repository: https://github.com/RowthCodes/testautomation-playwright-mvp
- Primary languages: TypeScript (Playwright) and C#

## Table of contents
- [Project overview](#project-overview)
- [Repository layout](#repository-layout)
- [Prerequisites](#prerequisites)
- [Getting started](#getting-started)
- [Running tests](#running-tests)
- [Project conventions](#project-conventions)
- [Adding tests](#adding-tests)
- [CI / recommended workflow](#ci--recommended-workflow)
- [Useful links](#useful-links)
- [Contributing](#contributing)
- [License](#license)

## Project overview
This repository demonstrates a minimal setup to run Playwright tests written in TypeScript and also includes a .NET solution for C# test examples. Use the TypeScript Playwright tests for modern JS/TS-based automation and the C# solution for teams using .NET test frameworks. The configuration and manifest files are included so you can run tests locally and adapt the setup for CI.

## Repository layout
Important files and folders in the repository:

- [.gitignore](https://github.com/RowthCodes/testautomation-playwright-mvp/blob/main/.gitignore) — files and folders to ignore in Git.
- [QATestSuite.sln](https://github.com/RowthCodes/testautomation-playwright-mvp/blob/main/QATestSuite.sln) — .NET solution (C#) for example tests.
- [package.json](https://github.com/RowthCodes/testautomation-playwright-mvp/blob/main/package.json) — Node/Yarn scripts and dependencies for Playwright tests.
- [playwright.config.ts](https://github.com/RowthCodes/testautomation-playwright-mvp/blob/main/playwright.config.ts) — Playwright test runner configuration.
- [tsconfig.json](https://github.com/RowthCodes/testautomation-playwright-mvp/blob/main/tsconfig.json) — TypeScript configuration.
- [yarn.lock](https://github.com/RowthCodes/testautomation-playwright-mvp/blob/main/yarn.lock) — Yarn lockfile.
- scripts/ — helper scripts (see folder in repo).
  - https://github.com/RowthCodes/testautomation-playwright-mvp/tree/main/scripts
- tests-playwright/ — Playwright TypeScript test sources and helpers.
  - https://github.com/RowthCodes/testautomation-playwright-mvp/tree/main/tests-playwright
- tests-csharp/ — C# test projects and assets.
  - https://github.com/RowthCodes/testautomation-playwright-mvp/tree/main/tests-csharp

## Prerequisites
- Node.js (recommended LTS >= 16)
- Yarn or npm (Yarn recommended if you want to use the included yarn.lock)
- Playwright (browsers installed) — installed via the Playwright CLI
- (Optional) .NET SDK for C# tests (if you plan to run projects in `tests-csharp`)

## Getting started (TypeScript Playwright)
1. Clone the repository:
   git clone https://github.com/RowthCodes/testautomation-playwright-mvp.git
   cd testautomation-playwright-mvp

2. Install dependencies:
   - Using Yarn:
     yarn install
   - Using npm:
     npm install

3. Install Playwright browsers:
   - Using npx:
     npx playwright install
   - Or using Yarn:
     yarn playwright install

4. (Optional) Confirm configuration files:
   - [playwright.config.ts](https://github.com/RowthCodes/testautomation-playwright-mvp/blob/main/playwright.config.ts)
   - [tsconfig.json](https://github.com/RowthCodes/testautomation-playwright-mvp/blob/main/tsconfig.json)

## Running tests

Playwright (TypeScript)
- Run all Playwright tests:
  - npx playwright test
  - or yarn playwright test
- Run a single test file:
  - npx playwright test tests-playwright/path/to/test.spec.ts
- Open Playwright interactive test runner / inspector:
  - npx playwright test --ui
- Run in headed mode for debugging:
  - npx playwright test --headed --debug

C# (.NET)
- Restore and run the solution (from repository root):
  - dotnet restore QATestSuite.sln
  - dotnet test QATestSuite.sln
- Open the solution in Visual Studio / Rider to run and debug tests.

Notes:
- Check package.json for available scripts and customize as needed: https://github.com/RowthCodes/testautomation-playwright-mvp/blob/main/package.json
- Adjust the Playwright config for browser choices, timeouts, and reporters in: https://github.com/RowthCodes/testautomation-playwright-mvp/blob/main/playwright.config.ts

## Project conventions
- Tests are organized under `tests-playwright` for TypeScript Playwright and `tests-csharp` for .NET/C# examples.
- Keep page object / helper code separate from test files to improve reuse and readability.
- Use environment variables or a config file (not committed) for any sensitive values (credentials, API keys). Do not store secrets in the repo.

## Adding tests
- TypeScript Playwright:
  - Add new spec files under `tests-playwright/` following `*.spec.ts` naming.
  - Add reusable page objects or fixtures under a `lib/` or `pages/` subfolder.
- C#:
  - Add new test projects to the `QATestSuite.sln` or add test classes under `tests-csharp/`.

## CI / recommended workflow
- Use a CI pipeline (GitHub Actions, GitLab CI, etc.) to:
  - Install Node / Yarn and .NET (if running C# tests)
  - Install Playwright browsers: npx playwright install --with-deps
  - Run linter / compile TypeScript: npx tsc --noEmit
  - Run Playwright tests: npx playwright test --reporter=dot (or generate HTML/JUnit)
  - Collect test artifacts (screenshots, videos, traces) from Playwright for failed tests
- Keep CI job matrix small (browsers and platforms you care about) and keep jobs isolated.

## Useful links
- Playwright docs: https://playwright.dev/
- Playwright CLI (install browsers): npx playwright install

## Contributing
Contributions are welcome. Suggested workflow:
- Fork the repo
- Create a feature branch
- Add tests and/or improvements
- Open a PR with a descriptive title and details of changes

## Contact / Maintainer
Repository owner: RowthCodes — https://github.com/RowthCodes
