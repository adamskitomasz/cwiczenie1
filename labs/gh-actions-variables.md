
- Copy content of this snipet to your repository into .github/workflows

```

name: Test actions and scheduleres/triggers  # ${{ github.workflow }}
on:
  push:

jobs:
  debug_variables:    # Action
    runs-on: ubuntu-20.04
    steps:
    - name: check Variables   # steps
      run: |
        # echo ${{ env.my_fav_ubuntu }}
        # echo ${{ github.repository }}
        # echo ${{ github.workflow }}
        # echo $GITHUB_SHA
        # echo $GITHUB_WORKSPACE
        # echo $GITHUB_REF
        # echo "Debug actor:  $GITHUB_ACTOR"
        echo "User more Variables from: " 
        echo "https://docs.github.com/en/actions/learn-github-actions/environment-variables#default-environment-variables"



          