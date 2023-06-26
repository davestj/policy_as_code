# Implementing Policy-as-Code in Azure

## Prerequisites

Before getting started, make sure you have the following prerequisites:

- Azure subscription
- Azure command-line interface (CLI) installed
- Familiarity with Azure Resource Manager (ARM) templates and Policy-as-Code concepts
- Access to Azure Active Directory (AAD) and Intune for MFA and Intune configuration

## Step 1: Clone this repo and edit the ARM Template

The ARM template consists of two policy definitions: one for enforcing the tag name-value pair policy, and the other for enforcing the MFA and Intune registration policy for the "Engineering" group.

## Step 2: Deploy the ARM Template

To deploy the ARM template and enforce the policies, follow these steps:

1. Open a command-line interface (CLI) and sign in to your Azure account.

2. Navigate to the directory where the `BasePolicy_intune.yaml` template file is located.

3. Run the following command to deploy the template:

   ```bash
   az deployment group create --name <deployment_name> --resource-group <resource_group_name> --template-file BasePolicy_intune.yaml --parameters tagName=<tag_name> mfaGroupId=<mfa_group_object_id>
   ```

   Replace `<deployment_name>` with a name for your deployment, `<resource_group_name>` with the target resource group, `<tag_name>` with the desired tag name for the tag name-value pair policy, and `<mfa_group_object_id>` with the object ID of the "Engineering" group in Azure Active Directory.

4. The deployment process will start, and the ARM template will be applied to the specified resource group. Wait for the deployment to complete.

5. Once the deployment is successful, the policies will be enforced as specified in the template.
