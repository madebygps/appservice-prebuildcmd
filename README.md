# Pre-Build Command Configuration

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
