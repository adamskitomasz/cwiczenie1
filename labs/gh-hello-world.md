- To newly created repository add first Github action

- Copy content of this snipet to your repository into .github/workflows
```
name: hello

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v1
    - name: Run a one-line script
      run: echo Hello, world!
    - name: Run a multi-line script
      run: |
        echo Add other actions to build,
        echo test, and deploy your project.
```


- Now add and commit changes
```
git add .
git commit -m 'first action'
```
- Push the files to the remote.

        git push -u origin master

 - Browse to the repository on GitHub.com and reload the page to confirm the files have been properly pushed.

 - Check actions tab, and verify if workflow started
