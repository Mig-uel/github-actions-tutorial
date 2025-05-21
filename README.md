# Introduction to GitHub Actions

GitHub Actions is a powerful automation tool that allows you to create workflows for your software development processes. With GitHub Actions, you can automate tasks such as building, testing, and deploying your code directly from your GitHub repository.

## Contents

1. **Basic Concepts**

   - **Workflow**: A workflow is an automated process that you define in your GitHub repository. It consists of one or more jobs that run in response to specific events.
   - **Job**: A job is a set of steps that execute on the same runner. Each job runs in a fresh instance of the virtual environment.
   - **Step**: A step is an individual task that can run commands or actions. Steps can be actions or shell commands.
   - **Action**: An action is a reusable unit of code that can be used in workflows. Actions can be created by you or the community.
   - **Runner**: A runner is a server that runs your workflows when triggered. GitHub provides hosted runners, or you can host your own.
   - **Event**: An event is a specific activity that triggers a workflow. Examples include pushing code, creating a pull request, or scheduling a job.
   - **Trigger**: A trigger is an event that starts a workflow. You can define triggers in your workflow file.
   - **Environment**: An environment is a set of resources that your workflow can access. You can define environments for different stages of your deployment process.
   - **Secret**: A secret is a sensitive piece of information, such as an API key or password, that you can store in your repository settings and use in your workflows without exposing it in your code.

2. **Chaining Jobs Together in a Workflow**

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

## Credits

Video series: [Introduction to GitHub Actions](https://youtube.com/playlist?list=PLiO7XHcmTsleVSRaY7doSfZryYWMkMOxB&si=wqMOf9krw8grDRjt) by [Mickey Gousset](https://www.youtube.com/@MickeyGousset) on YouTube.
