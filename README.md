# Introduction to GitHub Actions

GitHub Actions is a powerful automation tool that allows you to create workflows for your software development processes. With GitHub Actions, you can automate tasks such as building, testing, and deploying your code directly from your GitHub repository.

## Contents

**1. GitHub Actions Basics**

- **Workflow**: A workflow is an automated process that you define in your GitHub repository. It consists of one or more jobs that run in response to specific events.

- **Job**: A job is a set of steps that execute on the same runner. Each job runs in a fresh instance of the virtual environment.

- **Step**: A step is an individual task that can run commands or actions. Steps can be actions or shell commands.

- **Action**: An action is a reusable unit of code that can be used in workflows. Actions can be created by you or the community.

- **Runner**: A runner is a server that runs your workflows when triggered. GitHub provides hosted runners, or you can host your own.

- **Event**: An event is a specific activity that triggers a workflow. Examples include pushing code, creating a pull request, or scheduling a job.

- **Trigger**: A trigger is an event that starts a workflow. You can define triggers in your workflow file.

- **Environment**: An environment is a set of resources that your workflow can access. You can define environments for different stages of your deployment process.

- **Secret**: A secret is a sensitive piece of information, such as an API key or password, that you can store in your repository settings and use in your workflows without exposing it in your code.

**2. Chaining Jobs Together in a Workflow**

- You can chain jobs together in a workflow by using the `needs` keyword. This allows you to specify that one job depends on the successful completion of another job before it runs.

  - Example:

    ```yaml
    jobs:
      build:
        runs-on: ubuntu-latest
        steps:
          - name: Checkout code
            uses: actions/checkout@v2
          - name: Build project
            run: echo "Building project..."

      test:
        runs-on: ubuntu-latest
        needs: build
        steps:
          - name: Checkout code
            uses: actions/checkout@v2
          - name: Run tests
            run: echo "Running tests..."
    ```

**3. The GitHub Context Object and Variables**

- Every time you execute a workflow, GitHub provides a context object that contains information about the workflow run and the environment in which it is running.

- The GitHub context object provides information about the workflow run, including the event that triggered it, the repository, and the actor who triggered it.

- You can access context variables using `${{ github.<context_variable> }}` syntax.
- Example:

  ```yaml
  jobs:
    build:
      runs-on: ubuntu-latest
      steps:
        - name: Print GitHub context
          run: echo "Event: ${{ github.event_name }}"
  ```

- You can use this information in your workflow if you need to make decisions based on the context of the workflow run.

- You can also define your own variables using the `env` keyword. These variables can be accessed in your steps using `${{ env.<variable_name> }}` syntax.

  - Example:

    ```yaml
    jobs:
      build:
        runs-on: ubuntu-latest
        env:
          MY_VARIABLE: "Hello, World!"
        steps:
          - name: Print variable
            run: echo "Variable: ${{ env.MY_VARIABLE }}"
    ```

- You can define environment variables at the job level, step level, or workflow level. The scope of the variable depends on where you define it.

- You can also output variables from one job to another using the `outputs` keyword. This allows you to pass data between jobs in a workflow.

  - Example:

    ```yaml
    jobs:
      build:
        runs-on: ubuntu-latest
        steps:
          - name: Set output variable
            id: set_output
            run: echo "::set-output name=my_output::Hello, World!"

      test:
        runs-on: ubuntu-latest
        needs: build
        steps:
          - name: Use output variable
            run: echo "Output: ${{ needs.build.outputs.my_output }}"
    ```

## 4. The GitHub Actions Marketplace

- The GitHub Actions Marketplace is a collection of pre-built actions that you can use in your workflows. You can find actions for various tasks, such as deploying to cloud providers, sending notifications, and more.

- You can search for actions in the marketplace and add them to your workflow by specifying the action's repository and version.

  - Example:

    ```yaml
    jobs:
      build:
        runs-on: ubuntu-latest
        steps:
          - name: Checkout code
            uses: actions/checkout@v2
          - name: Use an action from the marketplace
            uses: actions/setup-node@v2
            with:
              node-version: '14'
    ```

- You can also create your own actions and publish them to the marketplace for others to use. Actions can be written in JavaScript, Docker, or as a composite action.

- [GitHub Actions Marketplace](https://github.com/marketplace?type=actions)

## 5. Run a Workflow Against a Pull Request

- You can configure your workflow to run against pull requests by using the `pull_request` event as a trigger. This allows you to run tests and checks on code changes before they are merged into the main branch.

  - Example:

    ```yaml
    on:
      pull_request:
        branches:
          - main

    jobs:
      build:
        runs-on: ubuntu-latest
        steps:
          - name: Checkout code
            uses: actions/checkout@v2
          - name: Run tests
            run: echo "Running tests..."
    ```

## Credits

[Introduction to GitHub Actions](https://youtube.com/playlist?list=PLiO7XHcmTsleVSRaY7doSfZryYWMkMOxB&si=wqMOf9krw8grDRjt) by [Mickey Gousset](https://www.youtube.com/@MickeyGousset) on YouTube.
