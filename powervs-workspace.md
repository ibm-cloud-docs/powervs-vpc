---

copyright:
  years: 2023
lastupdated: "2023-12-05"

keywords:

subcollection: powervs-vpc

---

{{site.data.keyword.attribute-definition-list}}

## Prerequisites
{: #powervs-workspace-prerequisites}

1. [Confirm your {{site.data.keyword.cloud_notm}} settings](https://cloud.ibm.com/docs/powervs-vpc?topic=powervs-vpc-powervs-automation-planning#vpc-cloud-prereqs)
2. [Set the IAM permissions](https://cloud.ibm.com/docs/powervs-vpc?topic=powervs-vpc-powervs-automation-planning#powervs-automation-IAM-prereqs)
3. [Create an SSH key Pair](https://cloud.ibm.com/docs/powervs-vpc?topic=powervs-vpc-powervs-automation-planning#powervs-automation-ssh-key)

## Deploying the Power Virtual Server with VPC landing zone - 'PowerVS Workspace' Variation
{: #powervs-automation-deploy}

To deploy the Power Virtual Server with VPC landing zone through the IBM Cloud console:

1. Go to the IBM Cloud catalog and search for 'Power Virtual Server with VPC landing zone'. Click the tile.
1. Select the latest version.
1. Select **Create a new architecture** for a new deployment or **Extend Power Virtual Server with VPC landing zone** to extend existing deployment with new PowerVS workspace
1. Select the **PowerVS Workspace** variation. 
1. Click **Review deployment options**.
    - Select **Add to project** to add this deployment to an IBM Cloud project and combine it with other deployments. IBM Cloud projects include several additional pipeline steps before deployment, including deployment validation, cost calculation, compliance verification and approval process.
    - Select **Create from the CLI** to get the CLI command. With that command you can trigger the deployment from the CLI.
    - Select **Work with code** to embed the code into other terraform deployments.
    - Select **Deploy with IBM Cloud Schematics** to trigger deployment process directly.

Edit the configuration by entering the **Required input variables**. **Optional input variables** are for advanced configuration and for deeper customization of the provisioned elements. You should know exactly what is the change goal and result by modifying the optional input variables. 
- Input parameters are described in the [readme file](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure/blob/main/solutions/full-stack/README.md){: external} for a new architecture deployment and in the [readme file](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure/blob/main/solutions/extension/README.md){: external} for extending existing deployment with new PowerVS workspace.
- Secure input parameters might be entered directly or might be referenced from an existing {{site.data.keyword.secrets-manager_full_notm}}. For more information, see [Storing arbitrary secrets](/docs/secrets-manager?topic=secrets-manager-arbitrary-secrets).

The deployment typically can take up to 60 minutes but might take longer depending on the performance of {{site.data.keyword.cloud_notm}} components.
{: note}

## Validating the deployment
{: #validate-deployment}

After you provision an instance, verify the success of the deployment by:

- Checking the log files in {{site.data.keyword.bplong_notm}}. There shouldn't be any errors.
- Trying out the access to the bastion host by using an SSH key. Access should be possible. 
- Logging to all created VPC and PowerVS instances. Access should be possible.

## Next steps
{: #powervs-automation-next}

You can connect to the landscape by using following SSH command:

```sh
ssh -A -o ServerAliveInterval=60 -o ServerAliveCountMax=600 -o ProxyCommand=\"ssh -W %h:%p root@\<access_host_floating_ip\>\" root@\<vpc_instance_ip\>
```

