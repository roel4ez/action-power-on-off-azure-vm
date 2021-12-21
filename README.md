# action-power-on-off-azure-vm

A reusable GitHub action that turns on/off or deallocates an Azure VM.

## Details

You will need a Service Principal on Azure with `Contributor` access to the
Resource Group the VM belongs to. This [article](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli)
documents on how to create Service Principals.

The action requires 6 different parameters:

- `AZURE_VM_NAME`: The name of the VM in Azure you want to turn on/off
- `AZURE_RG_NAME`: The Resource Group in which the VM lives
- `POWER_SWITCH`: string indicating if you want power `ON` or `OFF`, or `DEALLOCATE`
- `AZURE_SP_CLIENTID`: The AppId/ClientID of the Service Principal
- `AZURE_SP_SECRET`: The secret of the ServicePrincipal
- `AZURE_TENANTID`: TenantID where the ServicePrincipal belongs to.

## Example

See the [main-flow.yml](.github/workflows/main-flow.yml) for an example on how
to use this.
