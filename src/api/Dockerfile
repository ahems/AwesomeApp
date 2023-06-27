FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /api

# Copy everything
COPY . ./
# Restore as distinct layers
RUN dotnet restore
# Build and publish a release
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /api
COPY --from=build-env /api/out .

EXPOSE 80

#ENV AZURE_COSMOS_ENDPOINT=https://<myCosmosAccount>.documents.azure.com:443
#ENV APPLICATIONINSIGHTS_CONNECTION_STRING=
ENV AZURE_COSMOS_DATABASE_NAME=Todo
ENTRYPOINT ["dotnet", "Todo.Api.dll"]