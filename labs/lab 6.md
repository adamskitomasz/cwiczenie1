- To newly created repository add new Github actions

- Copy content of this snipet and add required values for matrix strategy to your repository into .github/workflows

In this example we would like to use multiple versions of file as parameter.

Check documentation for matrix strategy:
https://docs.github.com/en/actions/using-jobs/using-a-build-matrix-for-your-jobs#example-running-multiple-versions-of-nodejs

In our case, variable name in matrix should be "version"

```
name: artifacts-matrix

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
       include:
         - value1
         - value2 
    steps:
         - name: Create a file
           run: echo ${{ matrix.version }} > my_file_${{ matrix.version }}.txt
         - name: Accidentally upload to the same artifact via multiple jobs
           uses: actions/upload-artifact@v3
           with:
               name: my-artifact
               path: ${{ github.workspace }}
```
```
        git add .
        git commit -m 'matrix artifacts'
```


- Push the files to the remote.

        git push -u origin master

 - Browse to the repository on GitHub.com and reload the page to confirm the files have been properly pushed.

 - Check actions tab, and verify if workflow started
