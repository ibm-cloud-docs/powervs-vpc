---

copyright:
  years: 2024
lastupdated: "2024-03-06"

keywords:

subcollection: powervs-vpc

---

{{site.data.keyword.attribute-definition-list}}

# Prerequisites
{: #powervs-Prerequisites}
1. [Confirm your {{site.data.keyword.cloud_notm}} settings](https://cloud.ibm.com/docs/powervs-vpc?topic=powervs-vpc-powervs-automation-planning#vpc-cloud-prereqs)
2. [Set the IAM permissions](https://cloud.ibm.com/docs/powervs-vpc?topic=powervs-vpc-powervs-automation-planning#powervs-automation-IAM-prereqs)
3. [Create an SSH key Pair](https://cloud.ibm.com/docs/powervs-vpc?topic=powervs-vpc-powervs-automation-planning#powervs-automation-ssh-key)

For more information about prerequisites [learn here](https://cloud.ibm.com/docs/powervs-vpc?topic=powervs-vpc-powervs-automation-planning)

## Deploying the Power Virtual Server with VPC landing zone - 'PowerVS quickstart' variation
{: #powervs-quickstart-deploy}

To deploy the Power Virtual Server with VPC landing zone through the IBM Cloud&reg; console:

1. Go to the [IBM Cloud catalog](https://cloud.ibm.com){: external} and search for 'Power Virtual Server with VPC landing zone'. Click the tile.
2. Select the latest product version.
3. Select **Create a new architecture** for a new deployment.
4. Select the **PowerVS Quickstart** variation.
5. Click **Review deployment options**.
    - Select **Add to project** to add this deployment to an IBM Cloud project and combine it with other deployments. IBM Cloud projects includes several additional pipeline steps before deployment, including deployment validation, cost calculation, compliance verification and approval process.
    - Select **Create from the CLI** to get the CLI command. With that command you can trigger the deployment from the CLI.
    - Select **Work with code** to embed the code into other terraform deployments.
    - Select **Deploy with IBM Cloud Schematics** to trigger deployment process directly.

Edit the configuration by entering the **Required input variables**. **Optional input variables** are for advanced configuration and for deeper customization of the provisioned elements. You should know exactly what is the change goal and result by modifying the optional input variables. 
- Input parameters are described in the following readme files:
  - [Quickstart readme file](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure/blob/main/solutions/quickstart/README.md#inputs){: external} for a new architecture deployment.
- Secure input parameters might be entered directly or might be referenced from an existing {{site.data.keyword.secrets-manager_full_notm}}. For more information, see [Storing arbitrary secrets](/docs/secrets-manager?topic=secrets-manager-arbitrary-secrets).

The deployment typically can take up to 20 minutes but might take longer depending on the performance of {{site.data.keyword.cloud_notm}} components.
{: note}

## Validating the deployment
{: #validate-deployment}

After you provision an instance, verify the success of the deployment by:

- Checking the log files in {{site.data.keyword.bplong_notm}}. There shouldn't be any errors.
- Trying out the access to the bastion host by using a SSH key. Access should be possible. 
- Logging to all created VPC and PowerVS instances. Access should be possible.

## Next steps
{: #powervs-automation-next}

You can connect to the landscape by using following SSH command:

- To connect to the PowerVS instance:
    ```sh
    ssh -A -o ServerAliveInterval=60 -o ServerAliveCountMax=600 -o ProxyCommand=\"ssh -W %h:%p root@\<access_host_floating_ip\>\" root@\<powervs_instance_management_ip\>
    ```
- To connect to the NFS/NTP/DNS/Proxy Intel VSI:
  ```sh
    ssh root@\<access_host_floating_ip\>
    ```
