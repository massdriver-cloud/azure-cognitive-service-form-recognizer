## Azure Cognitive Service Form Recognizer

Azure Cognitive Service Form Recognizer is a cloud-based service that uses machine learning technology to identify and extract text, key-value pairs, and table data from form documents with a high degree of accuracy. This service is particularly useful for automating data entry and processing, as it reduces the need for manual data extraction.

### Design Decisions

When setting up the Azure Cognitive Service Form Recognizer, several design decisions have been considered to optimize its deployment and usage:
- **Service Tier**: The `sku_name` variable allows you to select the appropriate service tier based on your performance and cost requirements.
- **Location**: The `location` variable ensures that the service is provisioned in the desired Azure region for better performance and compliance with data residency requirements.
- **Custom Subdomain**: The `custom_subdomain_name` variable is customizable for better identification and DNS resolution.
- **Tags**: The `tags` variable can be configured to include metadata tags for better resource management and cost allocation.

### Runbook

#### Unable to Access Form Recognizer Endpoint

This section addresses issues where the Form Recognizer endpoint is not accessible. It outlines how to validate the endpoint using Azure CLI commands.

Check the Cognitive Service Form Recognizer account details:

```sh
az cognitiveservices account show \
    --name {ServiceName} \
    --resource-group {ResourceGroupName}
```

You should see details of the Cognitive Service account, including the endpoint URL. Make sure the endpoint URL is correct and accessible from your network.

#### Authentication Issues

This section helps you verify and troubleshoot authentication issues that may arise when accessing the Cognitive Service Form Recognizer.

Check if the service principal has the necessary roles:

```sh
az role assignment list \
    --assignee {ServicePrincipalId}
```

Ensure that the role `Cognitive Services User` is assigned at the right scope. If not, assign the role as follows:

```sh
az role assignment create \
    --assignee {ServicePrincipalId} \
    --role "Cognitive Services User" \
    --scope /subscriptions/{subscriptionId}/resourceGroups/{ResourceGroupName}/providers/Microsoft.CognitiveServices/accounts/{AccountName}
```

#### Network Connectivity Problems

Problems with network connectivity to the Cognitive Service Form Recognizer endpoint can be common. This section addresses how to diagnose these issues.

Ping the endpoint to check for connectivity:

```sh
ping {FormRecognizerEndpoint}
```

You should see a response from the endpoint. If the request times out, it indicates a network connectivity issue that may require further network troubleshooting steps or checks for firewall rules.

#### Troubleshooting Form Recognizer Responses

Sometimes, the service might not return the expected responses. This section helps diagnose such issues by inspecting the service logs.

Use the Azure Portal to access logs:

1. Navigate to your Form Recognizer resource.
2. Go to "Diagnostic settings".
3. Ensure you have configured diagnostic logs to be stored in a storage account, event hub, or Log Analytics workspace.

Analyze logs for any warning or error messages that can indicate the root cause of the problem.

