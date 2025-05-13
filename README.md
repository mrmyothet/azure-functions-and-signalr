# SignalR with Azure Functions Triggers and Bindings

Enable automatic updates in a web application using Azure Functions and SignalR

| **Property**     | **Value**                                                                                                                                                                                                                     |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Page Type**    | Sample                                                                                                                                                                                                                        |
| **Languages**    | JavaScript, TypeScript, Node.js                                                                                                                                                                                               |
| **Products**     | Azure, Azure Cosmos DB, Azure Functions, Azure SignalR, Azure Storage, VS Code                                                                                                                                                |
| **URL Fragment** | `azure-functions-and-signalr-javascript`                                                                                                                                                                                      |
| **Name**         | Enable real-time updates in a web application using Azure Functions and SignalR Service                                                                                                                                       |
| **Description**  | Change a JavaScript web app update mechanism from polling to real-time push-based architecture with SignalR Service, Azure Cosmos DB, and Azure Functions. Use Vue.js and JavaScript to use SignalR using Visual Studio Code. |

This repository is the companion to the following training module:

- [Enable automatic updates in a web application using Azure Functions and SignalR Service](https://learn.microsoft.com/training/modules/automatic-update-of-a-webapp-using-azure-functions-and-signalr/)

This solution displays fake stock prices as they update:

- [Start](./start): uses polling every minute
- [Solution](./solution): uses database change notifications and SignalR

## Set up resources

The Azure resources are created from bash scripts in the `setup-resources` folder. This includes creating:

- Azure Cosmos DB
- Azure SignalR
- Azure Storage (for Azure Function triggers)

## Ports

- Client: 3000: built with webpack
- Server: 7071: build with Azure Functions core tools

## Starting project without SignalR

The starting project updates stock prices in a Cosmos DB database every minute with an Azure Function app and a timer trigger. The client polls for all the stock prices.

## Ending project

The starting project updates stock prices in a Cosmos DB database every minute with an Azure Function app and a timer trigger. The client uses SignalR to recieve on the Cosmos DB items with change notifications through an Azure Functions app.

## Deploy to Azure Static Web Apps and Azure Functions App

1. Deploy the backend to Azure Functions App.

2. Deploy the frontend to Azure Static Web Apps in Standard plan type (not free) in order to use [bring your own backend](https://learn.microsoft.com/azure/static-web-apps/functions-bring-your-own) (byob).

   - Azure Cloud: Choose the Vue.js prebuild template then edit for this example, using the [example client workflow](example-client-workflow.yml). The build relies on the injection of the repo variable to find the BACKEND_URL value during SWA build and deploy. The webpack Dotenv param for `systemvars: true` brings in the value from the GitHub step to the webpack build.

   - Local: The client build on the local machine depends on a `.env` file at the root of the client application.

3. In Azure Functions, enable CORS for the client URL and check `Enable Access-Control-Allow-Credentials`.

## Resources

- [Azure SignalR service documentation](https://learn.microsoft.com/azure/azure-signalr/)
- [Azure SignalR service samples](https://github.com/aspnet/AzureSignalR-samples)
- [Azure Functions triggers and bindings for SignalR](https://learn.microsoft.com/azure/azure-functions/functions-bindings-signalr-service)
