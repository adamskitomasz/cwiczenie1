- Copy content of this snipet to your repository into .github/workflows
```
name: Environment Variables
env:
  WORKSPACE_ENVIRONMENT_VARIABLE: 'custom workspace environment variable'
on: [push]
jobs:
  ubuntu:
    env:
      JOB_ENVIRONMENT_VARIABLE: 'custom job environment variable for ubuntu'
    runs-on: ubuntu-latest
    steps:
      - name: Print custom environment variables from ubuntu-latest
        env:
          STEP_ENVIRONMENT_VARIABLE: 'custom step environment variable for bash'
        run: |
          echo "Accessing environment variables in run command"
          echo "$WORKSPACE_ENVIRONMENT_VARIABLE"
          echo "$JOB_ENVIRONMENT_VARIABLE"
          echo "$STEP_ENVIRONMENT_VARIABLE"
          echo "------------------------------------------------------"
          echo "Accessing environment variables using env context"
          echo "${{ env.WORKSPACE_ENVIRONMENT_VARIABLE }}"
          echo "${{ env.JOB_ENVIRONMENT_VARIABLE }}"
  windows:
    env:
      JOB_ENVIRONMENT_VARIABLE: 'custom job environment variable for windows'
    runs-on: windows-latest
    steps:
      - name: Print custom environment variables from windows-latest
        env:
          STEP_ENVIRONMENT_VARIABLE: 'custom step environment variable for powershell'
        run: |
          echo "Accessing environment variables in run command"
          echo "$Env:WORKSPACE_ENVIRONMENT_VARIABLE"
          echo "$Env:JOB_ENVIRONMENT_VARIABLE"
          echo "$Env:STEP_ENVIRONMENT_VARIABLE"
          echo "------------------------------------------------------"
          echo "Accessing environment variables using env context"
          echo "${{ env.WORKSPACE_ENVIRONMENT_VARIABLE }}"
          echo "${{ env.JOB_ENVIRONMENT_VARIABLE }}"
```

- Now add and commit changes
```
git add .
git commit -m 'environment variables'
```
- Push the files to the remote.

        git push -u origin master

 - Browse to the repository on GitHub.com and reload the page to confirm the files have been properly pushed.

 - Check actions tab, and verify if workflow started
