## Welcome
Tomasz Adamski

## Breaks:
**45-50min-10min break**

## What we need to start:
1. Github account - created with @gds.ey.pl email
2. VSCode
3. Git Bash
4. 50mb free space on disk (-_-)


---

# Core concepts of a GitHub Action:
## Why care about Github Actions? (presentation)
- Automate, customize, and execute your software development workflows right in your repository with GitHub Actions. You can discover, create, and share actions to perform any job you'd like, including CI/CD, and combine actions in a completely customized workflow.
## Core concepts (presentation)
5 cases where we ca use feature like github actions
* deployment
* testing
* lack of devops/appadmin
* we have to use Azure but we cannot access to client console
* PM
---    
# 10 words about YAML
- 2 spaces instead of 4 :)
- YAML to JSON - show off
- other usecase of yml
- yml validator
- what we dont do in yml
- copy paste with white marks
- lists
- yaml validator 
--- 
# Exercises with  GitHub Actions key features
## Configuring a workflow
- You only need a GitHub repository to create and run a GitHub Actions workflow.
### Show: 
- simple workflow with 1env, 1need

## Building first workflows
### Show: 
- sets\gh-actions-hello-world.yml
- show in github actions - logs
### Lab: 
- labs\lab 1.md
- 10 min to try
- send hello, check npm

### Show: 
- sets\gh-actions-check-console.yml
- show in github actions - logs
### Lab: 
- lab\gh-action-check-console.md
- 10 min to try
- Run simple code with result to logs

**First break**

### Show: Actions from Github/Azure
- when we use Actions insted of jobs
[...]more info: https://docs.github.com/en/actions/creating-actions/about-custom-actions

## Triggers
### Show: 
- sets\gh-actions-triggers.yml
[...]more info: https://docs.github.com/en/actions/using-workflows/triggering-a-workflow#using-a-single-event
- exceptions

## Variables
- env. (show levels and how to use it)
- steps. / step id (how to use output from steps)
- what is ${{ GITHUB_TOKEN }}
- when we use ${{ GITHUB_TOKEN }}

### Show: 
- sets\gh-actions-variables.yml
### Lab: 
- lab\gh-actions-variables.md
- try to find and test some GitHub Variables 
- reuse YAML form lab to say hello to You

#   Continuous Integration with GitHub Actions
- Building and validating the project
### Show: 
- sets\gh-build-app.yml
#   Uploading artifact
### Show: 
- sets\gh-actions-create-file.yml
- Go to GH and show how it looks
### Lab:
- lab\gh-actions-create-file.md

#   Creating a GitHub release/matrix
- labs: labs\gh-matrix.md
- Go to GH and show how it looks
- Show at least 2 artifacts
[...]more info: https://docs.github.com/en/actions/using-jobs/using-a-matrix-for-your-jobs
---
# Continuous Deployment with GitHub Actions
## Preparing secrets in repository
### Show
- Go to GH and show how it looks
### Lab
- labs\lab 4.md 

# Preparing Azure Webapp in your subscription
### Show: How to set WebApp Service

# Deploying application to Webapp
- Show: Connect to GitHub from Web App Azure Service
- Show: Prepared Workflow prepared by Azure
- Check commits from Azure
- Deploy express app
- Redeploy with Azure and Redeploy with VSCode
