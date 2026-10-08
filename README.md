# Build the same Azure environment every time

One ARM template (`environment.json`) that builds a small environment in a resource group:

- an Azure Static Web App (Free plan)
- a storage account (Standard_LRS, Hot access tier, secure transfer only, minimum TLS 1.2, anonymous blob access off)
- a Log Analytics workspace (30 days of logs)

One parameter, `environment` (`test` or `prod`), decides the names and the `environment` tag. Everything else is
the same, so test and production come out identical.

## Deploy it in the Azure portal (no command line)

1. Azure portal: search **Deploy a custom template** (Custom deployment).
2. **Build your own template in the editor** → **Load file** → choose `environment.json` → **Save**.
3. Pick your subscription, **Create new** resource group (for example `rg-tailwind-orders-test`), a region,
   and the environment `test`.
4. **Review + create** → **Create**. It takes under half a minute.
5. Repeat with a new resource group and `prod` for production.

Run it again on the same resource group and nothing changes. Change a setting by hand (for example the storage
account's default access tier) and redeploy (resource group → **Deployments** → the latest run → **Redeploy**):
the setting goes back to what the file says. Incremental mode (the default) leaves alone anything that is not in
the file.

## Cost and clean-up

The Static Web App is on the Free plan; storage and Log Analytics are pay-as-you-go and cost next to nothing while
empty. Delete the resource groups when you are done.

## Learn more

- What are ARM templates? https://learn.microsoft.com/azure/azure-resource-manager/templates/overview
- Deploy with the Azure portal: https://learn.microsoft.com/azure/azure-resource-manager/templates/deploy-portal
- Deployment modes: https://learn.microsoft.com/azure/azure-resource-manager/templates/deployment-modes

From the video "Infrastructure as Code Explained Simply" on Hassan | Enterprise AI & DevOps.
