# AZ-204 Notes and Projects

## App Services

To create the webapp resource groups, app service plan and app service run (within the app repository):

```
$ az webapp up --runtime PYTHON:3.9 --sku B1 --logs
```

since the web app is hosted within this repo (not in it's own repo), we need to change the startup command so gunicorn knows where to find the flask application object:

```
$ az webapp config set --resource-group $RESOURCE_GROUP --name $APP_NAME --startup-file "gunicorn --bind=0.0.0.0 --timeout 600 --chdir app-service/msdocs-python-flask-webapp-quickstart app:app"
```

To setup CI/CD with github actions, use the `azure/webapps-deploy` action and add publish profile secret to the repository (can be downloaded from the [portal](https://docs.microsoft.com/en-us/azure/app-service/deploy-github-actions?tabs=applevel#configure-the-github-secret))

## Function Apps

Durable function bootstrapped with the [VS Code Functions Extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions) `Azure Functions` commands (from the command palette).

Minimum three functions needed for durable function:

1. Start Function - normal function with a trigger (e.g. HTTP)
2. Orchestrator - calls the activity functions
3. Activity Functions(s) - do the actual work
