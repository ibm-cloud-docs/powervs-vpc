---

copyright:
  years: 2023, 2024
lastupdated: "2024-01-22"

keywords:

subcollection: powervs-vpc

---

{{site.data.keyword.attribute-definition-list}}

# Deploying the Power Virtual Server with VPC landing zone - 'Import PowerVS Workspace' Variation
{: #deploy-powervs-import-workspace}

To deploy an IBMCloud Schematics Workspace that imports existing VPC and Power Virtual Server Workspace resources through the IBM Cloud console:

1. Go to the IBM Cloud catalog and search for 'Power Virtual Server with VPC landing zone'. Click the tile.
1. Select the latest version.
1. Select **Create a new architecture** for a new deployment.
1. Select the **Import PowerVS Workspace** variation. 
1. Click **Review deployment options**.
    - Select **Add to project** to add this deployment to an IBM Cloud project and combine it with other deployments. IBM Cloud projects include several additional pipeline steps before deployment, including deployment validation, cost calculation, compliance verification and approval process.
    - Select **Create from the CLI** to get the CLI command. With that command you can trigger the deployment from the CLI.
    - Select **Work with code** to embed the code into other terraform deployments.
    - Select **Deploy with IBM Cloud Schematics** to trigger deployment process directly.

Edit the configuration by entering the **Required input variables**. **Optional input variables** are for advanced configuration and for deeper customization of the provisioned elements. You should know exactly what is the change goal and result by modifying the optional input variables. 
- Input parameters are described in the [readme file](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure/blob/main/solutions/import-workspace/README.md){: external} for importing existing VPC and PowerVS workspace resources.
- Secure input parameters might be entered directly or might be referenced from an existing {{site.data.keyword.secrets-manager_full_notm}}. For more information, see [Storing arbitrary secrets](/docs/secrets-manager?topic=secrets-manager-arbitrary-secrets).

The deployment typically can take up to 10 minutes depending on the performance of {{site.data.keyword.cloud_notm}} components.
{: note}

## Validating the deployment
{: #validate-powervs-import-workspace}

After you provision an instance, verify the success of the deployment by:

- Checking the log files in {{site.data.keyword.bplong_notm}}. There shouldn't be any errors. 
- Checking if all required VPC and PowerVS resource details are mentioned in the terraform output.

## Next steps
{: #next-steps-powervs-import-workspace}

Deploy the deployable architecture ['Power Virtual Server for SAP HANA'](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-sap-9aa6135e-75d5-467e-9f4a-ac2a21c069b8-global) on top of this solution.
