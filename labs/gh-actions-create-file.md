- Copy content of this snipet to your repository into .github/workflows
- Mind to fix path of myvar in steps
```

name: Create some artifacts with actions from marketplace  # ${{ github.workflow }}
on:
  push:

env:
  my_var: ....

jobs:
  debug_variables:    # Action
    runs-on: ubuntu-20.04
    steps:
    - uses: actions/checkout@v2

    - run: mkdir -p artifacts

    - run: echo ${{my_var}} > artifacts/word.txt # fix my_var here

    - run: echo ......... >> artifacts/word.txt # here place  echo 'date'  to append current date to file 

    - uses: actions/upload-artifact@v3
      with:
        name: my-artifact
        path: artifacts/word.txt