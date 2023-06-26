# Implementing Policy-as-Code in Azure

## Prerequisites

Before getting started, make sure you have the following prerequisites:

- Azure subscription
- Azure command-line interface (CLI) installed
- Familiarity with Azure Resource Manager (ARM) templates and Policy-as-Code concepts

## Step 1: Clone this repo and edit the ARM Template

- In this template, we define a policy (`enforceTaggingPolicy`) that checks if all resources have a specified tag with a specific name-value pair. 
- If a resource does not have the required tag or the tag value is incorrect, the policy denies the creation or modification of the resource. 
- We also assign the policy to the Engineering group and ensure that users from that group have MFA enabled.

## Step 2: Deploy the ARM Template

To deploy the ARM template and enforce the policy, follow these steps:

1. Open a command-line interface (CLI) of your choice.

2. Sign in to Azure using the Azure CLI:

   ```bash
   az login
   ```

3. Set the appropriate subscription where you want to deploy the resources:

   ```bash
   az account set --subscription <subscription_id>
   ```

4. Create a resource group:

   ```bash
   az group create --name <resource_group_name> --location <location>
   ```

   Replace `<resource_group_name>` with the name of your resource group and `<location>` with the desired Azure region.

5. Deploy the ARM template:

   ```bash
   az deployment group create --resource-group <resource_group_name> --template-file BasePolicy.yaml --parameters tagName=<tag_name> tagValue=<tag_value> engineeringGroupObjectId=<engineering_group_object_id>
   ```

   Replace `<resource_group_name>` with the name of your resource group, `<tag_name>` and `<tag_value>` with the desired tag name and value, and `<engineering_group_object_id>` with the Object ID of the Engineering group.

6. Wait for the deployment to complete. Once the deployment is successful, the policy will be enforced, and the Engineering group will have MFA enabled.
