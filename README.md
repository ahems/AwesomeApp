# AwesomeApp
My Awesome To-Do List App

Install NPM: https://nodejs.org/en/download
Install dotnet 6: https://dotnet.microsoft.com/en-us/download/dotnet/6.0

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
  "AZURE_COSMOS_ENDPOINT":"https://<myCosmosAccount>.documents.azure.com:443",
  "AZURE_COSMOS_DATABASE_NAME" : "Todo",
  "APPLICATIONINSIGHTS_CONNECTION_STRING" : "<your connection string>"
}
```

Start the API like this:
```
cd src\api
dotnet run
```

For the Web site, create a `.env` file within the base of the `\src\web\src` folder with the following configuration:

```
REACT_APP_API_BASE_URL https://localhost:3101
REACT_APP_APPLICATIONINSIGHTS_CONNECTION_STRING <your connection string>
```

From the `\src\web' Folder:
npm ci
npm start
