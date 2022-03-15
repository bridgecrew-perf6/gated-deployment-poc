# gated-deployment-poc
GitHub Actions gated deployment proof of concept.

*** Work in progress ***

## GitHub Actions Workflows
| Workflow | Trigger | Action Performed |
| ------------- | ------------- | ------------- |
| ```.github\workflows\deploy-dev.yml```  | On Push to the '```develop```' branch | Builds code, runs tests and then deploys to the Development environment |
| ```.github\workflows\deploy-test.yml```  | Manually triggered | Builds code, runs tests and then deploys to the Test environment <br/><br/> Note: workflow will only execute against the ```develop``` branch |
| ```.github\workflows\deploy-prod.yml```  | Manually triggered | Builds code, runs tests and then deploys to the Production environment. <br/><br/> Note: workflow will only execute against the ```main``` branch |

## Setup
1. Create following 'GitHub Environments' via the Project Settings page.
    * production
    * test
    * development
<br/><br/>
2. Run the below command in the Azure Portal Cloud Shell to create the Azure app registration used for github actions deployment
    ```
    az ad sp create-for-rbac --name GatedDeploymentPocGithubActions --role contributor --scopes /subscriptions/XXXXX-XXXXX-XXXXX-XXXXX-XXXXX/resourceGroups/gated-deployment-poc --sdk-auth
    ```

3. Create Github project secret '```AZURE_CREDENTIALS```' for each GitHub Environment. This should be set to the JSON string returned by the command from the previous step.

4. Create Github project secret '```AZURE_RESOURCE_GROUP_NAME```' for each GitHub Environment. This should be set to the name of the Resource Group containing the Azure Static Web App Resource e.g. gated-deployment-poc. The Resource Group needs to be pre-created before running the deployment workflow.

5. Create Github project secret '```AZURE_STATIC_WEB_DEPLOY_KEY```' for each GitHub Environment containing the Static Web App Deployment Key. The Static Web App should be created in the above mentioned Resource Group before running the deployment workflow.
