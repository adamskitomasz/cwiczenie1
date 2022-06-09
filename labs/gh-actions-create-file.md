---
name: Create some artifacts with actions from marketplace  # ${{ github.workflow }}
on:
  push:
  # schedule:
  # - cron: "0/10 9-17 * * MON-FRI"

env:
  my_github: tomad4
  repo_name: my-beautiful-proj # $GITHUB_WORKSPACE
  my_fav_ubuntu: ubuntu-20.04 
  my_repository: tomad4/my-beautiful-proj # $GITHUB_REPOSITORY

jobs:
  debug_variables:    # Action
    runs-on: ubuntu-20.04
    steps:
    - uses: actions/checkout@v2

    - run: mkdir -p artifacts

    - run: echo "Results of file test, if you see this it meand it is ok" > artifacts/word.txt

    - run: echo ${{}} > artifacts/word.txt

    - uses: actions/upload-artifact@v3
      with:
        name: my-artifact
        path: artifacts/word.txt