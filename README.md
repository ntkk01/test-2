# Playwright Automated Testing

# Description

This is the official documentation for setting up and running automated tests using Playwright and TypeScript. The tests are designed to cover various functionalities of the Nova Platform application.
Tech Stack

    Language: TypeScript
    Testing Framework: Playwright
    CI/CD Integration: GitHub Actions (or other CI services)
  # Setting up the development environment

Step 1: Install Node.js and npm

Before installing Playwright and TypeScript, ensure that Node.js and npm (Node Package Manager) are installed on your system.
**For macOS:**

    Open the terminal.
    Install Homebrew if you don’t have it installed yet:

    bash

/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

Install Node.js using Homebrew:

bash

brew install node

Verify the installation:

bash

    node -v
    npm -v

**For Windows**:

    Download the Node.js installer from the Node.js official website.
    Install Node.js by following the installation.
    Open PowerShell or cmd and verify the installation:

    bash

    node -v
    npm -v

Step 2: Set Up a New Project

Now that Node.js and npm are installed, let’s set up a new project.

    Open your terminal or PowerShell.
    Create a new directory for your project and navigate to it:

    bash

mkdir playwright-test
cd playwright-test

Initialize a new npm project:

bash

    npm init -y

    This command will create a package.json file that tracks your project's dependencies.

Step 3: Install Playwright and TypeScript
1. Install Playwright:

bash

npm install -D playwright

This installs Playwright as a dev dependency. After installation, install the required browsers for Playwright:

bash

npx playwright install

2. Install TypeScript and types for Node.js:

bash

npm install -D typescript @types/node

This installs TypeScript and type definitions for Node.js.

3. Create a tsconfig.json file:

After installing TypeScript, create the TypeScript configuration file:

bash

touch tsconfig.json

Add the following configuration to tsconfig.json:

json

{
  "compilerOptions": {
    "target": "ESNext",
    "module": "commonjs",
    "lib": ["ESNext", "DOM"],
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  },
  "include": ["tests/**/*.ts"]
}

Step 4: Create Playwright Configuration

You also need to set up Playwright configuration to define how your tests will run in different browsers.

    Create a Playwright config file:

    bash

touch playwright.config.ts

Open the playwright.config.ts file and add the following configuration:

typescript

    import { defineConfig } from '@playwright/test';

    export default defineConfig({
      testDir: './tests',
      retries: 2,  // Number of retries for failed tests
      use: {
        headless: true,  // Run tests in headless mode
        viewport: { width: 1280, height: 720 },  // Set viewport size
        screenshot: 'only-on-failure',  // Take screenshots on failure
        video: 'retain-on-failure',  // Record video on failure
      },
      projects: [
        {
          name: 'chromium',
          use: { browserName: 'chromium' },
        },
        {
          name: 'firefox',
          use: { browserName: 'firefox' },
        },
      ],
    });

Step 5: Writing a Test

    Create a directory for your tests:

    bash

mkdir tests

Inside the tests directory, create your first test file:

bash

touch tests/example.spec.ts

Add the following content to example.spec.ts:

typescript

    import { test, expect } from '@playwright/test';

    test('basic test', async ({ page }) => {
      await page.goto('https://example.com');
      const title = await page.title();
      expect(title).toBe('Example Domain');
    });

This is a basic test that navigates to example.com and checks the title of the page.
Step 6: Running the Tests

Now that everything is set up, you can run your tests using Playwright.

    To run all tests, execute:

    bash

npx playwright test

To run tests in a specific browser (e.g., Chromium):

bash

    npx playwright test --project=chromium



bash

git remote add origin <repository_URL>
git push -u origin main

   
