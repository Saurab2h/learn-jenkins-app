# Copilot Instructions for Learn Jenkins App

## Project Overview
This is a simple React application bootstrapped with Create React App, designed for learning Jenkins CI/CD pipelines. It includes unit tests (Jest), end-to-end tests (Playwright), and automated deployment to Netlify.

## Architecture
- **Frontend**: Single-page React app with minimal components (App.js as main component)
- **Build**: Uses `react-scripts` for bundling; output goes to `build/` directory
- **Testing**: Jest for unit tests, Playwright for e2e tests against served build
- **CI/CD**: Jenkins pipeline handles build, parallel testing, and Netlify deployment

## Key Workflows
- **Development**: `npm start` runs dev server on localhost:3000
- **Build**: `npm run build` creates production bundle in `build/`
- **Unit Tests**: `npm test` runs Jest with JUnit output to `test-results/junit.xml`
- **E2E Tests**: `npx playwright test` after serving build on port 3000
- **CI Pipeline**: See `jenkinsfile` for Docker-based stages (Node 18 Alpine for build/tests, Playwright image for e2e)

## Conventions and Patterns
- **App Versioning**: Displayed in UI as "Application version: X" where X comes from `REACT_APP_VERSION` env var (defaults to '1')
- **Test Reporting**: Unit tests use `jest-junit` for CI integration; e2e uses Playwright's HTML and JUnit reporters
- **E2E Setup**: Tests expect app served on localhost:3000; use `npx serve -s build -l 3000` for local e2e testing
- **CI Environment**: Set `CI_ENVIRONMENT_URL` for Playwright baseURL in CI (defaults to localhost:3000)

## Examples
- Update app version: Set `REACT_APP_VERSION=2` before build to change displayed version
- Run full test suite locally: `npm run build && npx serve -s build -l 3000 & npx wait-on http://localhost:3000 && npx playwright test`
- Add new e2e test: Place in `e2e/` directory, follow pattern in `e2e/app.spec.js` (check title, link visibility, version)

## Key Files
- `jenkinsfile`: Defines CI pipeline with build, test, and deploy stages
- `playwright.config.js`: Configures e2e tests with retries on CI, HTML/JUnit reporting
- `package.json`: Scripts for build/test; jest-junit config for test output
- `src/App.js`: Main component displaying logo, Udemy link, and version</content>
<parameter name="filePath">/workspaces/learn-jenkins-app/.github/copilot-instructions.md