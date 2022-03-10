# List of Azure cli commands 

##### For Resource Group

   ```sh
   // Command to create

      az group create --name ProgramFiction ResourceGroup --location southindia
   
   // Command to see resource groups in your subscription
     
      az group list
   
   // Show one group
   
      az group show --name ProgramFictionGroup
   
   // Delete Resource group

      az group delete --name ProgramFictionGroup

   // Deploy Resource Group

      az storage account create --resource-group ProgramFictionGroup --name ProgramFictionstore --location southndia --sku Standard_LRS --kind StorageV2
   
   // To deploy an ARM template or Bicep file

      az deployment group create --resource-group ProgramFictionGroup --template-file storage.bicep

   ```
