# Re-generating the markdown file for the chat conversation
# GitHub Actions Learning Session

## Introduction  
User wants to learn GitHub Actions, starting with the basics.  

---

## What is GitHub Actions?  
GitHub Actions is a CI/CD tool that lets you automate tasks like building, testing, and deploying your code right from your GitHub repository. It uses YAML files to define workflows.  

### Key Concepts:  
1. **Workflow**: Automated process defined in a YAML file (e.g., `.github/workflows/ci.yml`).  
2. **Job**: A set of steps executed on the same runner (like a virtual machine).  
3. **Step**: An individual task, like running a script or installing dependencies.  
4. **Runner**: The environment where the job runs (GitHub-hosted or self-hosted).  
5. **Event**: Triggers the workflow (e.g., `push`, `pull_request`).  

---

## Creating a Basic Workflow  
We'll create a workflow that runs when you push code to your repository.  

### 1. Create a Folder and File:  
In your GitHub repository, create a folder:  

`.github/workflows`
Inside that, create a file named `ci.yml`.  

### 2. Add Basic YAML Configuration:  
```yaml
name: CI Workflow

on:
    push:
        branches:
            - main  # Runs on push to the main branch

jobs:
    build:
        runs-on: ubuntu-latest

        steps:
            - name: Checkout code
                uses: actions/checkout@v2

            - name: Set up Node.js
                uses: actions/setup-node@v3
                with:
                    node-version: '16'

            - name: Install dependencies
                run: npm install

            - name: Run tests
                run: npm test
```

**Explanation:**

`name`: The workflow's name as it appears in the Actions tab.

`on`: Triggers the workflow. Here, it triggers on push to the main branch.

`jobs`: Defines jobs to run (here, only one job named build).

`runs-on`: Specifies the runner environment (using ubuntu-latest here).

**steps:**
- Checkout code using actions/checkout.
- Set up Node.js environment.
- Install dependencies using npm install.
- Run tests using npm test.

**Next Steps:**
- Commit and Push the file to your repository.
- Go to your GitHub repo and click on the Actions tab to see the workflow running.
