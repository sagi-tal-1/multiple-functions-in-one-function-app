# multiple-functions-in-one-function-app
Overview Azure Functions is a serverless compute service that enables you to run event-triggered code without having to explicitly provision or manage infrastructure. This repository provides an example of a Function App that hosts multiple functions, illustrating how to organize and manage them within a single app.
Features
Multiple Functions in One App: Demonstrates how to include several functions within a single Azure Function App.
Event Triggers: Examples of different types of event triggers such as HTTP, Timer, and Queue triggers.
Configuration Management: Guidance on managing configurations and settings for multiple functions.
Local Development and Debugging: Instructions for setting up and running the functions locally before deploying to Azure.
Getting Started
Prerequisites
Before you begin, ensure you have the following installed:

Azure CLI
Azure Functions Core Tools
Visual Studio Code or any preferred IDE
Node.js (if using JavaScript/TypeScript)
.NET SDK (if using C#)
Setup
Clone the Repository:

bash
Copy code
git clone https://github.com/yourusername/your-repo.git
cd your-repo
Install Dependencies:

bash
Copy code
npm install
# or for .NET
dotnet restore
Run Locally:

bash
Copy code
func start
Folder Structure
javascript
Copy code
├── HttpTriggerFunction
│   ├── index.js
│   ├── function.json
├── TimerTriggerFunction
│   ├── index.js
│   ├── function.json
├── QueueTriggerFunction
│   ├── index.js
│   ├── function.json
├── local.settings.json
└── host.json
HttpTriggerFunction: Contains an HTTP trigger function.
TimerTriggerFunction: Contains a Timer trigger function.
QueueTriggerFunction: Contains a Queue trigger function.
local.settings.json: Configuration file for local development.
host.json: Global configuration options for all functions.
Function Details
HTTP Trigger Function
This function is triggered by an HTTP request.

Location: HttpTriggerFunction/index.js
Trigger: HTTP GET/POST
javascript
Copy code
module.exports = async function (context, req) {
    context.log('HTTP trigger function processed a request.');
    const name = req.query.name || (req.body && req.body.name);
    const responseMessage = name
        ? `Hello, ${name}. This HTTP triggered function executed successfully.`
        : 'This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response.';

    context.res = {
        status: 200,
        body: responseMessage
    };
}
Timer Trigger Function
This function runs on a schedule.

Location: TimerTriggerFunction/index.js
Trigger: Timer (Cron expression)
javascript
Copy code
module.exports = async function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    if (myTimer.isPastDue) {
        context.log('Timer function is running late!');
    }
    context.log('Timer trigger function ran!', timeStamp);
}
Queue Trigger Function
This function processes messages from an Azure Storage Queue.

Location: QueueTriggerFunction/index.js
Trigger: Azure Storage Queue
javascript
Copy code
module.exports = async function (context, myQueueItem) {
    context.log('Queue trigger function processed work item', myQueueItem);
}
Deployment
Deploy to Azure
Login to Azure:

bash
Copy code
az login
Create a Resource Group:

bash
Copy code
az group create --name myResourceGroup --location westus
Create a Function App:

bash
Copy code
az functionapp create --resource-group myResourceGroup --consumption-plan-location westus --runtime node --functions-version 3 --name <YOUR_FUNCTION_APP_NAME> --storage-account <YOUR_STORAGE_ACCOUNT_NAME>
Deploy the Function App:

bash
Copy code
func azure functionapp publish <YOUR_FUNCTION_APP_NAME>
Contributing
Contributions are welcome! Please submit a pull request or open an issue to discuss improvements or bugs.

License
This project is licensed under the MIT License. See the LICENSE file for details.

