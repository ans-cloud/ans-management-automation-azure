# ANS Management Automation for Azure

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fans-cloud%2Fans-management-automation-azure%2Fmain%2FazureDeploy.json)


## How to deploy

Click the blue "Deploy to Azure" button

Or if you prefer commandline;
1. Clone the repository `git clone https://github.com/ans-cloud/ans-management-automation-azure.git`
2. Ensure you have [az cli](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) installed
3. Run `az login`
4. Switch to the correct subscription
```bash
az account set -s "YOUR_SUBSCRIPTION_ID"
```
5. Create a resource group (optional)
```bash
az group create \
  --name "name-for-resource-group" \
  --location "uksouth or another region of your choice"
```
6. Update the values in example.parameters.json (Optional)
6. Run the following command to deploy the ARM template
```bash
az deployment group create \
  --name "ans-management-automation-azure" \
  --resource-group "name-of-existing-resource-group" \
  --template-file "azureDeploy.json" \
  --parameters "example.parameters.json"
```


## What will this deploy?

This [ARM (Azure Resource Manager)](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/overview) template will deploy three [logicapps](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-overview) and an [Office365 Api Connection](https://docs.microsoft.com/en-us/azure/connectors/apis-list#managed-connectors), upon creation you can choose whether to use an existing or new [resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/overview#resource-groups)


## What do I need to do post deployment?

1. Navigate to your root management group (or each subscription manually)
2. Assign `Contributor` rights to the logicapp's [managed identity](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/howto-assign-access-portal)
3. Navigate to **API Connection** resource called Office365connection
4. Within the **API Connection** blade, select **Edit API Connection** from the menu
5. Click on the **Authorize** button and login with the Office365 account you want to send approval emails from. *Please note one authorised this connection can be used by anyone with access the Azure Portal and can be used to read and send emails so consider using a service user.*
