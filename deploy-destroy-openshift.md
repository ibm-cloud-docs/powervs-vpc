---

copyright:
  years: 2025
lastupdated: "2025-10-10"
subcollection: powervs-vpc
content-type: tutorial
account-plan: paid
completion-time: 1hour
keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Destroy resources deployed by the Deployable Architecture
{: #destroy-openshift}
{: toc-content-type="tutorial"}
{: toc-completion-time="1hour"}

In this tutorial, you'll learn how to destroy the resources deployed by the Quickstart OpenShift Variation of [{{site.data.keyword.powerSys_notm}} with VPC landing zone](/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global) Deployable Architecture when you don't need them anymore.

[Warning]{: tag-red} This will delete all the resources that were created by this deployment and result in total data loss of all data stored on these resources.

[Warning]{: tag-red} The **Quickstart OpenShift Variation** requires special clean up steps. If you deployed the **Standard Landscape** or **Quickstart** Variation, follow the steps in [Destroy using projects](/docs/secure-enterprise?topic=destroy-openshift) instead.
{: shortdesc}

## Prerequisites
{: #destroy-openshift-resources-prerequisites}

- You have an existing deployment of the Quickstart OpenShift Variation of [{{site.data.keyword.powerSys_notm}} with VPC landing zone](/catalog/architecture/deploy-arch-ibm-pvs-sap-9aa6135e-75d5-467e-9f4a-ac2a21c069b8-global) that you don't need anymore and want to destroy
- You have SSH access to the network services VSI in the landing zone via [Client to Site VPN](/docs/powervs-vpc?topic=powervs-vpc-solution-connect-client-vpn) or [Floating IP on the Jump Host](/docs/powervs-vpc?topic=powervs-vpc-solution-ssh)
- You have backed up all data that you will need in the future that is stored on the resources you're about to destroy
- You deployed using [Projects](/docs/secure-enterprise?topic=secure-enterprise-understanding-projects)
- You know the Ansible Vault password used for your deployment

## Destroy the Cluster resources
{: #destroy-openshift-cluster-resource}

1. Use SSH to log into the network services VSI.
1. Use Ansible Vault to decrypt the OCP config while you're using it. Make sure to encrypt it again after you're done.

    ```bash
    ansible-vault decrypt /root/.powervs/config.json
    ansible-vault encrypt /root/.powervs/config.json
    ```

1. Export your KUBECONFIG

    ```bash
    export KUBECONFIG=/root/ocp-powervs-deploy/auth/kubeconfig
    ```

1. Destroy the cluster resources. This process might take a while. If it fails due to time out, give it up to three retries. This step destroys the resources deployed by the IPI installer, including the PowerVS instances, DHCP subnets and application load balancers. From your home directory, run

    ```bash
    openshift-install destroy cluster  --log-level=debug  --dir=ocp-powervs-deploy/
    ```

1. Delete the Service IDs. Make sure to replace cluster_name with the name you used during deployment. From the ocp-powervs-deploy directory, run:

    ```bash
    export IBMCLOUD_API_KEY=<ibmcloud_api_key>
    ccoctl ibmcloud delete-service-id --credentials-requests-dir ./credreqs --name <cluster_name>
    ```

If something goes wrong during this step, **do not** proceed to destroying the project. It will fail and manual cleanup will be required. Instead, proceed to [troubleshooting](#destroy-openshift-troubleshooting) and open a support case if required.
{: tip}


## Destroy the Landing Zone resources
{: #destroy-openshift-landing-zone}

- By using the {{site.data.keyword.cloud_notm}} console:
    1.  Navigate to the **Configurations** inside your **Project**:
        1.  Click the **Navigation menu** icon ![Navigation menu icon](../icons/icon_hamburger.svg "Menu") > **Projects**.
        1.  Click on the project name. It will take you to an overview of your project.
        1.  Select the **Configurations** tab.

    1.  Undeploy the resources:
        1.  A project may consist of multiple configurations. Before you proceed, verify you're destroying the correct resources. You can do so by navigating to the **Resources** after clicking on the name of the **configuration**.
        1.  Once you clicked on the name of the configuration that contains the resources you want to destroy, it will show the status of the configuration under its name. The status should show as `Deployed` indicating the resources inside the configuration are active.
        1.  When you're sure you have the right resources, click the **Options** icon ![Options icon](../icons/action-menu-icon.svg "Options") > **Undeploy**
        1.  It will prompt you to enter the name of your configuration for confirmation.
        1.  The destroy process will begin and it should automatically take you back to the **Configurations** tab inside the **Project**.
            - This process may take a while.
            - The status of your configuration will change to `Undeploying...`.
            - If you ran into any issues during undeployment, please refer to the troubleshooting section in this tutorial
        1.  If you encounter any issues during this process, refer to the [troubleshooting](#destroy-openshift-troubleshooting) section


        You can access the logs by clicking on the status `Undeploying...` and clicking on the second line that says `Undeploying resources...`.
        {: tip}

        Alternatively, you can also follow the process in the related **Schematics workspace**, which you can easily access by clicking on the link under **Workspace** inside your configuration.
        {: tip}

    1.  Cleanup
        Once the Deployment status shows `-`, you can delete the configuration and if not required anymore also the project.
        1. Delete the **Configuration**:
            1.  In the **Configurations** tab inside the **Project**, select the **Options** icon ![Options icon](../icons/action-menu-icon.svg "Options") > `Delete`in the same row as your configuration and follow the instructions to complete deletion.
        1.  Once that's done, you can follow these steps to also delete the **Project** in case you don't have other **Configurations** in it:
            1.  Navigate back to all projects. You can do so by either clicking on **Projects** in the top left corner or via the **Navigation menu** icon ![Navigation menu icon](../icons/icon_hamburger.svg "Menu") > **Projects**.
            1.  Again select the **Options** icon ![Options icon](../icons/action-menu-icon.svg "Options") > `Delete Project`in the same row as your configuration and follow the instructions to complete the process.

## Troubleshooting
{: #destroy-openshift-troubleshooting}

If destroying the cluster resources failed, **do not** proceed to destroying the project. Instead, check out the following:
1. Check that you ran each command in the correct directory or passed the correct --dir argument.
1. If destroying the resources timed out, give it up to three retries. Each try may take a while.
1. If the above steps didn't help, proceed to open a support case and make sure to share the installation logs:
    1. ssh into the network services instance. Follow [Client to Site VPN](/docs/powervs-vpc?topic=powervs-vpc-solution-connect-client-vpn) or [Floating IP on the Jump Host](/docs/powervs-vpc?topic=powervs-vpc-solution-ssh) to learn more.
    1. Use the tool of your choice (e.g. scp) to copy `/root/ocp-powervs-deploy/.openshift_install.log` from the network services instance to your local machine.

If your destroy job failed, check out the following:
1. Examine logs. You can find them either in your project's configuration or in the related Schematics workspace.
1. Determine if there's a resource blocking your destroy process. There is a chance that modifications outside the automation are blocking the resource from getting deleted. Common examples are:
    - additional instances in the {{site.data.keyword.powerSys_notm}} workspace which block subnets from getting deleted
    - locked objects in cloud object storage that block the bucket's deletion
1. Try to clean up the resource that's blocking the destroy process from finishing.
1. Re-trigger the destroy process inside projects.
1. Should this not work, you may have to clean up the remaining resources manually. You can use the resource list and filter for resource group, prefix, and tags to easier locate the related resources (hint: you can find the prefix you defined during deployment inside your project configuration).
1. Should manual deletion of resources fail, navigate to the support center and open a ticket.
