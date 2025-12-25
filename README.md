# Playwright TypeScript Automation Project

## Table of Contents

1. [Project Overview](#project-overview)
2. [Prerequisites](#prerequisites)
3. [Installation](#installation)
4. [Project Structure](#project-structure)
5. [Running Tests](#running-tests)
6. [Tagging & Quarantine](#tagging--quarantine)
7. [Test Reports](#test-reports)
8. [CI/CD Integration](#cicd-integration)
9. [Best Practices](#best-practices)
10. [Troubleshooting](#troubleshooting)
11. [Contributing](#contributing)

---

## Project Overview

This repository contains **end-to-end automated tests** for [Your Application Name] using **Playwright with TypeScript**.
It supports **cross-browser testing** (Chromium, Firefox, WebKit), **parallel execution**, and **CI/CD pipeline integration**.

---

## Prerequisites

* Node.js >= 18.14.2
* npm >= 9.5
* Git
* IDE (VSCode recommended)
* Internet connection (to download browsers on first run)

---

## Installation

1. Clone the repository:

```bash
git clone https://github.com/your-org/your-project.git
cd your-project
```

2. Install dependencies:

```bash
npm install
```

3. Install Playwright browsers:

```bash
npx playwright install
```

---

## Project Structure

```
.
├── tests/               # Test scripts
│   ├── login.spec.ts
│   └── checkout.spec.ts
├── pages/               # Page Object Models
├── utils/               # Helper utilities
├── playwright.config.ts # Playwright configuration
├── package.json
└── README.md
```

---

## Running Tests

### Run all tests:

```bash
npx playwright test
```

### Run tests in headed mode (UI visible):

```bash
npx playwright test --headed
```

### Run a specific test file:

```bash
npx playwright test tests/login.spec.ts
```

### Run a specific test by name:

```bash
npx playwright test -g "should login successfully"
```

### Run tests in a specific browser:

```bash
npx playwright test --project=chromium
npx playwright test --project=firefox
```

---

## Tagging & Quarantine

### Tagging tests:

```ts
test('checkout flow', { tag: '@smoke' }, async ({ page }) => {});
test('flaky login', { tag: '@quarantine' }, async ({ page }) => {});
```

### Run only tagged tests:

```bash
npx playwright test --grep @smoke
```

### Exclude tagged tests (e.g., quarantine):

```bash
npx playwright test --grep-invert @quarantine
```

---

## Test Reports

Generate and view HTML report:

```bash
npx playwright show-report
```

Reports are generated automatically in the `playwright-report` folder after each run.

---

## CI/CD Integration

* Exclude quarantined tests: `--grep-invert @quarantine`
* Run in headless mode for CI: `--headed=false`
* Parallel execution to reduce run time: `--workers=4`
* Retry flaky tests: `--retries=2`
* Publish HTML reports after pipeline completion

Sample pipeline command:

```bash
npx playwright test --project=chromium --grep-invert @quarantine --workers=4 --retries=2
```

---

## Best Practices

* **Tag tests** for smoke, regression, or quarantine
* **Avoid hard-coded waits**; use `await page.waitForSelector()`
* **Use Page Object Model (POM)** for reusable selectors
* **Track flaky tests** and fix root cause
* **Keep test data externalized** (fixtures / JSON / APIs)

---

## Troubleshooting

* Browser not found: `npx playwright install`
* TypeScript errors: `npm run build`
* Tests failing locally but not in CI: Check environment variables and test data

---

## Contributing

1. Fork the repository
2. Create a feature branch
3. Add or fix tests
4. Raise a Pull Request with details
5. Ensure all tests pass before merge

---

**Author:** Your Name
**Date:** YYYY-MM-DD
**Project Version:** 1.0.0
