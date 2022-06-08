# - To newly created repository add new Github actions

# - Copy content of this snipet to your repository into .github/workflows

# Update snippet with missing fields. In this example we are looking for:

# Matrix strategy should use 2 parameters:

# ```
# - version: 10.x
# - version: 12.x
# ```

# Job environment variables should be:

# ```
#       name: new-artifact
# ```

# We should use upload artifact action for our artifact:

# ```
# actions/upload-artifact@v3
# ```


# Code snippet:
# ```
name: artifacts-complex

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:


    steps:
      - run: |
          mkdir -p ${{ github.workspace }}/artifact/${{ matrix.version }}
          echo hello,node version is ${{ matrix.version }} > ${{ github.workspace }}/artifact/${{ matrix.version }}/hello.txt
      - uses:
        with:
          name: ${{ env.name }}-name
          path: ${{ github.workspace }}/artifact/**/*
# ```
# ```
#         git add .
#         git commit -m 'complex artifacts'
# ```


# - Push the files to the remote.

#         git push -u origin master

#  - Browse to the repository on GitHub.com and reload the page to confirm the files have been properly pushed.

#  - Check actions tab, and verify if workflow started
