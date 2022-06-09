---
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


    - name: Checkout Code
      uses: actions/checkout@v2
      with:
        ref: ${{ github.head_ref }}   # checkout the correct branch name
        fetch-depth: 0                # fetch the whole repo history

    # - name: Git Version
    #   uses: codacy/git-version@2.2.0

  # create_file:
  #   runs-on: ubuntu-20.04
  #   steps:
  #   - name: Debug
  #     run: |
  #       curl google.pl | grep 301
    
  #   - name: Create file
  #     run: |
  #       echo "$(date)" > test.txt
  #       echo "Result: OK" >> test.txt
  #       cat test.txt
    

          