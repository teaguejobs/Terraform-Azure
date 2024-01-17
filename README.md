# Terraform-Azure
Sign in to the Azure Portal using the credentials provided for the lab.

Log In and Set Up the CLI
After logging in to Azure, select the Cloud Shell icon from the top menu bar and expand the terminal so it's easier to work with.
In the Welcome dialog, select Bash.
Select Show advanced settings and leave the default values.
Note: If your storage account details don't auto-populate, switch your Cloud Shell region to East US. Then, for Storage account, select Use existing.

Fill in the File share details:
Below File share, select Create new.
In the corresponding text box, enter terraform.
Click Create storage. The terminal takes a moment to initialize.
Download the zip file provided in the lab resources:
wget https://raw.githubusercontent.com/linuxacademy/content-terraform-2021/main/lab-managing-azure.zip
View the contents of the directory to verify the zip file downloaded:
ls
Unzip the file:
unzip lab-managing-azure.zip
View the contents of the directory again:
ls
You should now see a lab-managing-azure directory.
Change into the lab-managing-azure directory:
cd lab-managing-azure/
View the contents of this directory:
ls
You should see your main.tf file.
Edit the main.tf file:
vim main.tf
Update the virtual network's resource_group_name:
Above Cloud Shell, copy your Azure resource group name. You may need to pull down your Cloud Shell terminal to see it and you may need to change the location to match the lab.
To the right of the resource_group_name variable, replace <ADD YOUR RESOURCE GROUP> with your copied resource group name.
Write and quit to save your changes:
:wq!
Deploy the Infrastructure
Initialize your working directory so you can deploy your virtual network to Azure:
terraform init
Plan your test deployment:
terraform plan
Apply your test deployment:
terraform apply
When prompted, type "yes" to confirm the apply.
View the details of the virtual network resources Terraform is managing:
terraform show
View a list of the resources Terraform is managing:
terraform state list
You should now see that Terraform is managing 1 resource: azurerm_virtual_network.vnet.

Add a Subnet to the Configuration
Download the azure_resource_block.tf file provided in the lab resources:
wget https://raw.githubusercontent.com/linuxacademy/content-terraform-2021/main/azure_resource_block.tf
View the contents of the directory to ensure the file downloaded successfully:
ls
Edit the file:
vim azure_resource_block.tf
Update the subnet's resource_group_name:
Above Cloud Shell, copy your Azure resource group name.
To the right of the resource_group_name variable, replace <ADD YOUR RESOURCE GROUP> with your copied resource group name.
Write and quit to save your changes:
:wq!
Plan your configuration changes:
terraform plan
Apply your configuration changes:
terraform apply
When prompted, type "yes" to confirm the apply.
View the details of the resources Terraform is managing:
terraform show
This now includes the virtual network and subnet.
View a list of the resources Terraform is managing:
terraform state list
You should now see that Terraform is managing 2 resources: azurerm_virtual_network.vnet and azurerm_subnet.subnet.
Add a Tag to the Configuration
Edit the main.tf file:
vim main.tf
Copy the tags code provided in the lab resources.
Paste the tags code block below the resource code block so it's formatted as follows:
# Create a virtual network
resource "azurerm_virtual_network" "vnet" {
   name                = "BatmanInc"
   address_space       = ["10.0.0.0/16"]
   location            = "Central US"
   resource_group_name = "<YOUR_RESOURCE_GROUP_NAME>"
tags = {
   Environment = "TheBatcave"
   Team        = "Batman"
 }
}
Write and quit to save your changes:
:wq!
Ensure your Terraform files are formatted correctly:
terraform fmt
Plan your configuration changes:
terraform plan
Apply your configuration changes:
terraform apply
When prompted, type "yes" to confirm the apply.
View the details of the resources Terraform is managing:
terraform show
This now includes the virtual network, subnet, and tags.
Destroy the Infrastructure
Destroy the infrastructure:
terraform destroy
This will destroy all your managed resources, including the virtual network, subnet, and tags you used for testing.
When prompted, type "yes" to confirm the destroy.
Verify Terraform is no longer managing any resources:
terraform show
terraform state list
