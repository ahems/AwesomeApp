# AwesomeApp
My Awesome To-Do List App

Use this to give the VM running the API code permissions to the CosmosDB account:

```
resourceGroupName='<myResourceGroup>'
accountName='<myCosmosAccount>'
roleDefinitionId = '00000000-0000-0000-0000-000000000002' # Cosmos DB Built-in Data Contributor - https://learn.microsoft.com/en-us/azure/cosmos-db/how-to-setup-rbac#built-in-role-definitions
# Object (principal) ID of VM System-Assigned Identity
principalId = '<aadPrincipalId>'
az cosmosdb sql role assignment create --account-name $accountName --resource-group $resourceGroupName --scope "/" --principal-id $principalId --role-definition-id $roleDefinitionId
```

Update the appsettings.Development.json file like this:
```
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AZURE_COSMOS_ENDPOINT":"https://<myCosmosAccount>.documents.azure.com:443"
}
```
