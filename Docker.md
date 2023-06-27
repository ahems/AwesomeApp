# If using Docker!

Build them:

```
docker build -t awesomeapp:latest -f src/web/Dockerfile src/web
docker build -t awesomeapi:latest -f src/api/Dockerfile src/api
```

Run them:

```
docker run -it --rm -p 3100:80 awesomeapi:latest --env AZURE_COSMOS_ENDPOINT=https://<myCosmosAccount>.documents.azure.com:443 --env APPLICATIONINSIGHTS_CONNECTION_STRING=<appInsights>
docker run -it --rm -p 80:80 awesomeapp:latest --env ENV REACT_APP_API_BASE_URL=http://localhost:3100 --env REACT_APP_APPLICATIONINSIGHTS_CONNECTION_STRING=<appInsights>
```

Use AZ:

```
rg=rg-todo-csharp-cosmos-sql-dev
app=appi-uwlornlla2nuw
REACT_APP_APPLICATIONINSIGHTS_CONNECTION_STRING=$(az monitor app-insights component show --app $app -g $rg --query connectionString --output tsv)
APPLICATIONINSIGHTS_CONNECTION_STRING=$REACT_APP_APPLICATIONINSIGHTS_CONNECTION_STRING
AZURE_COSMOS_ENDPOINT=$(az cosmosdb list --resource-group $rg --query [0].documentEndpoint --output tsv)
AZURE_COSMOS_CONNECTION_STRING_KEY=$(az cosmosdb keys list --resource-group $rg --name $(az cosmosdb list --resource-group $rg --query [0].name --output tsv) --output json | jq -r '.primaryMasterKey')
```

Run using Environment variables:
```
docker run -it --rm -p 3100:80 awesomeapi:latest --env AZURE_COSMOS_ENDPOINT=$AZURE_COSMOS_ENDPOINT --env APPLICATIONINSIGHTS_CONNECTION_STRING=$APPLICATIONINSIGHTS_CONNECTION_STRING --env AZURE_COSMOS_CONNECTION_STRING_KEY=$AZURE_COSMOS_CONNECTION_STRING_KEY --env AZURE_COSMOS_DATABASE_NAME=Todo

docker run -it --rm -p 80:80 awesomeapp:latest --env REACT_APP_API_BASE_URL=http://localhost:3100 --env REACT_APP_APPLICATIONINSIGHTS_CONNECTION_STRING
```

Test API:
```
curl -L http://localhost:3100
```




  
