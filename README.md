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

## Usage

You can call this action from a workflow as follows:

```yml
name: Example workflow

on:
  workflow_dispatch:
    inputs:
      power:
        required: true
        description: 'Turn the VM ON or OFF'
        type: choice
        options:
          - 'ON'
          - 'OFF'
          - 'DEALLOCATE'
      vm_name:
        description: 'the name of the vm to be turned on'
        required: true 
        default: 'vm-test-gh-action'
        type: string
      rg_name:
        required: false
        type: string
        default: 'vm-test'
        description: 'the name of the resource-group the VM belongs to'

jobs:
  power_azure_vm:
    runs-on: ubuntu-latest
    steps:
      - name: Power Azure VM
        uses: roel4ez/action-power-on-off-azure-vm@v1.0.1
        with:
          AZURE_VM_NAME: ${{ github.event.inputs.vm_name }}
          AZURE_RG_NAME: ${{ github.event.inputs.rg_name }}
          POWER_SWITCH: ${{ github.event.inputs.power }}
          AZURE_SP_CLIENTID: ${{ secrets.AZURE_SP_CLIENTID }}
          AZURE_SP_SECRET: ${{ secrets.AZURE_SP_SECRET }}
          AZURE_TENANTID: ${{ secrets.AZURE_TENANTID }}
```
