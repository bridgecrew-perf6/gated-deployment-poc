# gated-deployment-poc
GitHub Actions gated deployment proof of concept

This is a work in progress.

## Setup
1. Create following GitHub environments
    * production
    * test
    * development
<br/><br/>
2. Run command in the Azure Portal Cloud Shell to create the Azure app registration used for github actions deployment
    ```
    az ad sp create-for-rbac --name GatedDeploymentPocGithubActions --role contributor --scopes /subscriptions/60de66df-f7bb-4ace-b572-2e0f466d7953/resourceGroups/gated-deployment-poc --sdk-auth
    ```

3. Create Github project secret 'AZURE_CREDENTIALS' for each GitHub Environment. Password should be set to the JSON output string returned by the command from the previous step.