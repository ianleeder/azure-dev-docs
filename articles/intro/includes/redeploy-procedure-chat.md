---
ms.custom: overview, devx-track-python
ms.topic: include
ms.date: 01/31/2024
ms.author: diberry
author: diberry
ms.service: azure
---

## Redeploy Chat app with load balancer endpoint

These are completed on the chat app sample. 

#### [Initial deployment](#tab/initial-deployment)

This process uses two different CLIs:

* Azure Developer CLI (AZD): 
    * Create environment for deployment
    * Deploy chat app 
* Azure CLI (AZ):
    * Run bash script to get Azure Container App ingress FQDN URL, which also uses AZD to set environment variables in deployment environment

1. Open the chat app sample's dev container using one of the following choices.

    |Language|Codespaces|Visual Studio Code|
    |--|--|--|
    |.Net|[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/Azure-Samples/azure-search-openai-demo-csharp)|[![Open in Dev Containers](https://img.shields.io/static/v1?label=Dev%20Containers&message=Open&color=blue&logo=visualstudiocode)](https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/azure-samples/azure-search-openai-demo-csharp)|
    |Java|[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/Azure-Samples/azure-search-openai-demo-java)|[![Open in Dev Containers](https://img.shields.io/static/v1?label=Dev%20Containers&message=Open&color=blue&logo=visualstudiocode)](https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/azure-samples/azure-search-openai-demo-java)|
    |JavaScript|[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/Azure-Samples/azure-search-openai-javascript)|[![Open in Dev Containers](https://img.shields.io/static/v1?label=Dev%20Containers&message=Open&color=blue&logo=visualstudiocode)](https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/azure-samples/azure-search-openai-javascript)|
    |Python|[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/Azure-Samples/azure-search-openai-demo)|[![Open in Dev Containers](https://img.shields.io/static/v1?label=Dev%20Containers&message=Open&color=blue&logo=visualstudiocode)](https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/azure-samples/azure-search-openai-demo)
|

1. Sign in to Azure Developer CLI (AZD).

    ```bash
    azd auth login
    ```

    Finish the sign in instructions.

1. Create an AZD environment with a name such as `chat-app`.

    ```bash
    azd env new <name>
    ```

1. To run [the bash script](https://github.com/Azure-Samples/azure-search-openai-demo/blob/main/scripts/load-balance-aca-setup.sh) to set the load balancer environment variables, sign in to the Azure CLI (AZ).

    ```bash
    az login --use-device-code
    ```

1. Run the following bash script to configure the chat app to use the load balancer.

    ```bash
    bash scripts/load-balance-aca-setup.sh <RESOURCE-GROUP-NAME> <CONTAINER-APP-URL>
    ```

    This script adds environment variables to instruct the chat app where to send requests to Azure OpenAI. 

1. Deploy the chat app.

    ```bash
    azd up
    ```

#### [Redeployment](#tab/redeployment)

This process uses two different CLIs:

* Azure Developer CLI (AZD): 
    * Deploy chat app 
* Azure CLI (AZ):
    * Run bash script to get Azure Container App ingress FQDN URL, which also uses AZD to set environment variables in deployment environment


1. Reopen the chat app sample's dev container using one of the following choices.

    |Language|Codespaces|Visual Studio Code|
    |--|--|--|
    |.Net|[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/Azure-Samples/azure-search-openai-demo-csharp)|[![Open in Dev Containers](https://img.shields.io/static/v1?label=Dev%20Containers&message=Open&color=blue&logo=visualstudiocode)](https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/azure-samples/azure-search-openai-demo-csharp)|
    |Java|[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/Azure-Samples/azure-search-openai-demo-java)|[![Open in Dev Containers](https://img.shields.io/static/v1?label=Dev%20Containers&message=Open&color=blue&logo=visualstudiocode)](https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/azure-samples/azure-search-openai-demo-java)|
    |JavaScript|[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/Azure-Samples/azure-search-openai-javascript)|[![Open in Dev Containers](https://img.shields.io/static/v1?label=Dev%20Containers&message=Open&color=blue&logo=visualstudiocode)](https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/azure-samples/azure-search-openai-javascript)|
    |Python|[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/Azure-Samples/azure-search-openai-demo)|[![Open in Dev Containers](https://img.shields.io/static/v1?label=Dev%20Containers&message=Open&color=blue&logo=visualstudiocode)](https://vscode.dev/redirect?url=vscode://ms-vscode-remote.remote-containers/cloneInVolume?url=https://github.com/azure-samples/azure-search-openai-demo)
|

1. Sign in to the Azure CLI (AZ).

    ```bash
    az login --use-device-code
    ```

1. Run the following bash script to configure the chat app to use the load balancer.

    ```bash
    bash scripts/load-balance-aca-setup.sh <RESOURCE-GROUP-NAME> <CONTAINER-APP-URL>
    ```

    This script adds environment variables to instruct the chat app where to send requests to Azure OpenAI. 

1. Deploy the chat app.

    ```bash
    azd up
    ```
    
    Wait until this process finishes before continuing.

---

You can now use the chat app with the confidence that it's built to scale across many users without running out of quota. 

