---
page_type: sample
languages:
- azdeveloper
- python
- bicep
- html
products:
- azure
- azure-app-service
urlFragment: azure-simple-fastapi-appservice
name: Deploy a minimal FastAPI Application on Azure App Service (Python)
description: A tiny, no-frills, template to deploy Python's FastAPI web framework to Azure App Service in the free tier.
---
<!-- YAML front-matter schema: https://review.learn.microsoft.com/en-us/help/contribute/samples/process/onboarding?branch=main#supported-metadata-fields-for-readmemd -->

# Simple FastAPI AZD Template

The most basic FastAPI "hello world" application as an AZD template ready for Azure App Service

![system diagram](diagram.png)

## Usage

1. Install AZD and run the following command to initialize the project.

```bash
azd init --template Azure-Samples/azd-simple-fastapi-appservice
```

This command will clone the code to your current folder and prompt you for the following information:

- `Environment Name`: This will be used as a prefix for the resource group that will be created to hold all Azure resources. This name should be unique within your Azure subscription.

2. Login to your Azure account.
```bash
azd auth login
```

3. Run the following command to build a deployable copy of your application, provision the template's infrastructure to Azure and also deploy the applciation code to those newly provisioned resources.

```bash
azd up
```

This command will prompt you for the following information:
- `Azure Location`: The Azure location where your resources will be deployed.
- `Azure Subscription`: The Azure Subscription where your resources will be deployed.

> NOTE: This may take a while to complete as it executes three commands: `azd package` (builds a deployable copy of your application), `azd provision` (provisions Azure resources), and `azd deploy` (deploys application code). You will see a progress indicator as it packages, provisions and deploys your application.

4. Then make changes to app.py and run `azd deploy` again to update your changes.

## Pre-Build Command Configuration

This repository explores how to configure Azure App Service pre-build commands to generate a `requirements.txt` file from `pyproject.toml` during the deployment process. This is particularly useful for Python projects using modern dependency management with Poetry or other tools that use TOML files.

### The Problem

Azure App Service's Python deployment process expects a `requirements.txt` file, but modern Python projects often use `pyproject.toml` for dependency management. We need a way to generate `requirements.txt` during deployment.

### Using pre_build_command

The pre-build command is configured to:
1. Read dependencies from `pyproject.toml`
2. Generate a `requirements.txt` file before App Service begins the deployment
3. Allow App Service to proceed with its standard Python dependency installation

To test this functionality:

1. Review the `prebuild.sh` script that handles the TOML to requirements.txt conversion
2. Deploy using:

```bash
azd deploy
```

This will trigger the pre-build process that generates the requirements.txt file before the main deployment starts.

### Current Status

This is an experimental repository documenting the investigation of pre-build command functionality in Azure App Service. See the commit history for evolution of the solution.

## Notes

This uses the F1 (free) SKU for app service, which has limited CPU and RAM resources.

See the [pricing calculator](https://azure.microsoft.com/en-au/pricing/calculator/) for details on paid SKUs replace the SKU option with a suitable choice.
