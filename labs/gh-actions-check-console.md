- Copy content of this snipet to your repository into .github/workflows
- Uncomment multiline "run" to test 
- try with "echo" someting that you want check - version of nuget, python, java etc.

```

name: Check different consoles

on: [push]

jobs: 
  shell-command:
    runs-on: ubuntu-18.04 # def: /bin/bash
    steps: 
      - name: Write so
        run: |
          # echo "Say hello to bash" 
          # echo $BASH_VERSION
      
      - name: multiline script with check npm
        run: | 
          # echo "123"
          # echo "456"
          # node -v
          # npm -v

  powershell-command:
    runs-on: windows-latest # def: Powershell
    steps: 
      - name: Write some
        run: |
          # echo "Say hello to Windows"
          # $PSVersionTable
      
      - name: Debug PS Get time with custom format
        run: |
          # Get-Date -format "yyyy--MM--dd HH:mm:ss"
          # $a = 1 ; echo $a

  python:
    runs-on: ubuntu-18.04
    steps: 
      - name: Write something
        run: python -V
      
      - name: Python GetDate but in python
        run: |
          # from datetime import date
          # today = date.today()
          # print("Today's date:", today)
        shell: python                      # if we need another shell we have to define