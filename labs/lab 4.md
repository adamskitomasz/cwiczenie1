- To newly created repository add secrets and Github actions

- Copy content of this snipet and add required lines to your repository into .github/workflows

Required lines:
 - workflow name
 - trigger
 - host
 - job name

```
    steps:
    - name: Azure login
      uses: azure/login@v1
      with:
        creds: ${{ secrets.creds }}
        allow-no-subscriptions: true
    - name: Azure cli
      run: az account show
```
        git add .
        git commit -m 'Azure login with secrets'
```
- Browse to the repository on GitHub.com and find tab "secrets". Add there one new secret with proper content:
```
{
  "clientId": "",
  "clientSecret": "",
  "tenantId": ""
}
```

- Push the files to the remote.

        git push -u origin master

 - Browse to the repository on GitHub.com and reload the page to confirm the files have been properly pushed.

 - Check actions tab, and verify if workflow started
