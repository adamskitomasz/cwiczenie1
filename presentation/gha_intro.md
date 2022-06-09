

# Introduction to GitHub Actions

### Agenda

1. Why care about Github Actions?
1. Core concepts
1. Configuring a workflow
1. Building first workflows

## Why care about Github Actions?

GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform that allows us to automate ours build, test, and deployment pipeline.

#### Build into Github:
Github Actions is fully integrated into Github and therefore doesn't require and external site. This means that it can be managed in the same place as all your other repository related features like pull requests and issues.


#### Multiple CI templates:
Github provides multiple templates for all kinds of CI (Continous Integration) configurations which make it extremely easy to get started. You can also create your own templates which you can then publish as an Action on the Github Marketplace.

#### Great free plan:
Actions are completely free for every open-source repository and include **2000 free build minutes per month** for all your private repositories.
If that is not enough for your needs you can pick another plan or go the **self-hosted** route


## Core concepts

#### Step:
A step is a set of tasks that can be executed by a job. Steps can run **commands or actions**.

#### Actions:
Actions are the smallest portable building block of a workflow and can be combined as steps to create a job.
You can create your own Actions or use publicly shared Actions from the Marketplace.

#### Job:
A job is made up of multiple steps and runs in an instance of the virtual environment.
Jobs can run:
 - independently
 -sequential if the current job depends on the previous job to be successful.

#### Workflow:
 A Workflow is an automated process that is made up of one or multiple jobs and can be triggered by an event.

#### Event:
Events are specific activities that trigger a workflow run.
workflow can be triggered when:
 - somebody pushes to the repository
 - pull request is created
 - listen to external events using Webhooks

#### Runner:
A runner is a machine with the Github Actions runner application installed.
Runners can be **hosted on Github or self-hosted** on your own machines/servers.


## Understanding the workflow file

#### Creating a workflow file:

Workflows can be created inside the **.github/workflows** directory by adding a **.yml** workflow file.

After creating the file you can start working on your workflow.

### General syntax:
Github Actions files are written using YAML syntax and have eighter a .yml or .yaml file extension. If you're new to YAML and want to learn more, I would recommend these two articles [Learn YAML in five minutes](https://www.codeproject.com/Articles/1214409/Learn-YAML-in-five-minutes) or [Introduction to YAML](https://dev.to/paulasantamaria/introduction-to-yaml-125f).

#### Understanding the workflow file


learn-github-actions.yml

```
name: learn-github-actions
on: [push]
env:
  CI: true
jobs:
  check-bats-version:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2
        with:
          node-version: '14'
      - run: npm install -g bats
      - run: bats -v
```
| Code        | Description           |
| ------------- |:-------------:|
| `name: learn-github-actions`      | Optional - The name of the workflow |
| `on: [push]`      | Specifies the trigger for this workflow.      |
|`env:`| Env defines a map of environment variables that are available to all jobs and steps in the workflow|
| `jobs:` | Groups together all the jobs that run in the learn-github-actions workflow. |
|`check-bats-version:`|Defines a job named check-bats-version. The child keys will define properties of the job.|
|`runs-on: ubuntu-latest`|Configures the job to run on the latest version of an Ubuntu Linux runner.|
|` steps:`|Groups together all the steps that run in the check-bats-version job.|
|` - uses: actions/checkout@v2`|The uses keyword specifies that this step will run v2 of the actions/checkout action.|
|` - run: npm install -g bats`|The run keyword tells the job to execute a command on the runner.|




#### Exercise: Create an example workflow

Go to labs/Lab 1.md file. (optional one)

Go To labs/Lab 2.md file.

#### Viewing the workflow's activity

1. On GitHub.com, navigate to the main page of the repository.


2. Under your repository name, click Actions.
![](img/1.jpg)

3. In the left sidebar, click the workflow you want to see.
![](img/2.jpg)

4. Under "Workflow runs", click the name of the run you want to see.
![](img/3.jpg)

5. View the results of each step.
![](img/4.jpg)



### Variables

Naming Considerations for Variables
GitHub Actions workflows allow you to define custom environment variables in a scoped workflow, job, or step. However, when defining your custom variables, there are a couple of things you must consider.

`GITHUB_ Prefix`
The GITHUB_ prefix is reserved for GitHub.

`Case Sensitivity`
GitHub variables are case sensitive.


https://docs.github.com/en/actions/learn-github-actions/environment-variables#default-environment-variables

Go to labs/Lab 3.md file.


### Secrets

Naming Secrets

`Characters`: Alphanumeric characters are used in secret names

`Unique`

`GITHUB_ Prefix`: You cannot use GITHUB_ in secret names

Go to labs/Lab 4.md file.

### Artifacts

When we execute a build or test run in a GitHub Actions workflow, it generates binaries and test results as the output of the workflow.
These items may be stored for the next jobs in the same workflow.
GitHub storage is utilized to store artifacts.
Usage is free for public repos and self-hosted runners.
Private repos have limitations on storage and the number of minutes to run actions.

Go to labs/Lab 5.md file.
Go to labs/Lab 6.md file.




# Continuous integration using GitHub Actions

### Agenda

1. Building and validating the project
1. Creating a GitHub release
1. Uploading artifact


## Getting hands-on with GitHub Actions


### Automate Build

1. Get the web project (<https://github.com/bireckimik/example-dot-net-app>)

1. Start workflow with event and environment variables

    ```yml
    name: Build and deploy ASP.NET Core app to Azure Web App

    on: [push]

    env:
      AZURE_WEBAPP_NAME: your_web_app_name    # set this to your application's name
      AZURE_WEBAPP_PACKAGE_PATH: '.'      
      DOTNET_VERSION: '3.1.201'        
    ```

1.  Initialize job, checkout code and build application

```yml
    jobs:
      build:
        runs-on: ubuntu-latest
        steps:


          - uses: actions/checkout@master


          - name: Setup .NET Core
            uses: actions/setup-dotnet@v1
            with:
              dotnet-version: ${{ env.DOTNET_VERSION }}


          - name: dotnet build and publish
            run: |
              dotnet build --configuration Release
              dotnet publish -c Release -o '${{ env.AZURE_WEBAPP_PACKAGE_PATH }}/myapp'
  ```

1. Upload artifact

    ```yml
    - name: Upload static site
      uses: actions/upload-artifact@v2
      with:
        name: artifact
        path: '${{ env.AZURE_WEBAPP_PACKAGE_PATH }}/myapp'
    ```


1. Create GitHub release

    ```yml
    - name: Create GitHub release
      id: create-new-release
      uses: actions/create-release@v1
      env:
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
      with:
        tag_name: ${{ github.run_number }}
        release_name: Release ${{ github.run_number }}
    ```



# Deploy applications to Azure using GitHub Actions

### Agenda

1. Setup Azure service principal and credentials
1. Prepare secrets in repository
1. Prepare Azure Webapp in your subscription - follow this document [Create Azure Web App](create_web_app.md)

### Automate Deploy

1. Add your Azure secrets like in Lab 4. Remember name of this secret, it will be used in next steps

1. Open file from previous exercise

1. Add new deploy job to existing workflow

    ```yml
    deploy:
      needs: [build]
      runs-on: ubuntu-latest
      steps:              # set this to the dot net version to use
    ```
1. Login to Azure Portal with your secrets.

   ```yml
   - name: Azure Login
     uses: azure/login@v1
     with:
       creds: ${{ secrets.AZURE_CREDENTIALS }}  ## Here should be name of your repository secret
   ```

1. Download artifact from previous job

      ```yml
      - name: Download site content
        uses: actions/download-artifact@v2
        with:
          name: artifact
          path: '${{ env.AZURE_WEBAPP_PACKAGE_PATH }}/myapp'
      ```

1. Deploy application to web app

      ```yml
      - name: 'Run Azure webapp deploy action '
        uses: azure/webapps-deploy@v2
        with:
          app-name: ${{ env.AZURE_WEBAPP_NAME }}
          package: '${{ env.AZURE_WEBAPP_PACKAGE_PATH }}/myapp'
      ```
#### Bonus: Github Actions workflow for generating presentation

Demo:

### Links

* <https://docs.github.com/actions/learn-github-actions/introduction-to-github-actions#understanding-the-workflow-file>
* <https://github.com/actions/upload-artifact>
* <https://github.com/actions/download-artifact>
* <https://docs.github.com/actions/reference/workflow-syntax-for-github-actions#jobsjob_idneeds>
* <https://github.com/actions/create-release>
* <https://docs.github.com/actions/reference/context-and-expression-syntax-for-github-actions#contexts>
* <https://github.com/marketplace/actions/zip-release>
* <https://github.com/actions/upload-release-asset>
* <https://docs.github.com/actions/guides/publishing-docker-images>
* <https://github.com/docker/build-push-action/tree/releases/v1>
* <https://docs.microsoft.com/azure/app-service/deploy-container-github-action>
* <https://github.com/azure/actions-workflow-samples>
* <https://github.com/azure/login>
* <https://github.com/azure/arm-deploy>
* <https://github.com/azure/webapps-deploy>

[filter-pattern-cheat-sheet] "https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#filter-pattern-cheat-sheet"

# Other useful apps
[GIT_DESKTOP] "https://desktop.github.com/"

# VSCode Extensions that I use:
**GitHubActions**: cschleiden.vscode-github-actions
**Git Blame**: waderyan.gitblame
**YAML**: redhat.vscode-yaml

[setup_env_for_azure]: https://docs.microsoft.com/en-us/azure/app-service/deploy-github-actions?tabs=applevel#configure-the-github-secret

# Cheat sheet:
[address_to_git_actions] "https://docs.github.com/en/actions"

# If you are too lazy or you are devops:
[cron_tab_cheater] "https://crontab.guru/"

# Some prepared runners 
**Language**	*Setup Action*
**.NET**	    *actions/setup-dotnet*
**ASP.NET**	    *actions/setup-dotnet*
**Java**	    *actions/setup-java*
**JavaScript**	*actions/setup-node*
**Python**	    *actions/setup-python*
## Thanks! Q&A
