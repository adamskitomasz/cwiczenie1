- To newly created repository add new Github actions

- Copy content of this snipet and add required action to your repository into .github/workflows

In this snippet, it is required to use upload artifact action. Here you can find documentation:

https://github.com/actions/upload-artifact#usage

```
name: artifacts

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - run: mkdir -p training/artifact/test

    - run: echo hello > training/artifact/test/file.txt

    - uses:
      with:
        name: first-artifact
        path: training/artifact/test/file.txt
```
```
        git add .
        git commit -m 'simple artifacts'
```


- Push the files to the remote.

        git push -u origin master

 - Browse to the repository on GitHub.com and reload the page to confirm the files have been properly pushed.

 - Check actions tab, and verify if workflow started
