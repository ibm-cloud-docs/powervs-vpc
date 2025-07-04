---

copyright:
   years: 2023, 2025
lastupdated: "2025-06-25"

keywords:

subcollection: powervs-vpc

---

{{site.data.keyword.attribute-definition-list}}

# Deploying a Power Virtual Server with VPC landing zone deployable architecture
{: #deploy}

You can deploy a deployable architecture from the {{site.data.keyword.cloud_notm}} catalog. You can choose one of several deployment options, including with {{site.data.keyword.cloud_notm}} projects. [Learn about IaC deployments with projects](/docs/secure-enterprise?topic=secure-enterprise-understanding-projects).

## Deploying with {{site.data.keyword.cloud_notm}} projects
{: #deploy-cloud}

To deploy a Power Virtual Server with VPC landing zone deployable architecture through the {{site.data.keyword.cloud_notm}} catalog, follow these steps:

1.  Make sure that you comply with the prerequisites in the [planning](/docs/powervs-vpc?topic=powervs-vpc-powervs-automation-prereqs) topic:
    - Have an {{site.data.keyword.cloud_notm}} API key.
    - Verify access roles.
    - **An SSH key which doesn't exist in target deployment region.**
1.  Go to the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external} and search for the architecture that you're interested in deploying:
    - **Power Virtual Server with VPC landing zone**
1.  Click the tile for the deployable architecture to open the details.
1.  Select the latest product version in the Architecture section.
1.  Select a variation, if more than one is available.
1.  Click **Review deployment options**.
1.  Select the **Add to project** deployment type in Deployment options, and then click **Add to project**.
    1.  Name your project, enter a description, and specify a configuration name. Click **Create**.
1.  Edit and validate the configuration:
    1.  Select your authentication method. You can use an existing secret in {{site.data.keyword.secrets-manager_short}} or add your API key directly. For more information, see [Using an API key or secret to authorize projects](/docs/secure-enterprise?topic=secure-enterprise-authorize-project).
    1.  Enter values for other required fields from the Required tab.
    1.  Optional: Specify other values from the Optional tab.
    1.  Save the configuration.
    1.  Click **Validate**. Validation takes a few minutes

        {{site.data.keyword.cloud_notm}} projects runs a Code Risk Analyzer scan that includes a [supported set of {{site.data.keyword.compliance_short}} rules](/docs/ContinuousDelivery?topic=ContinuousDelivery-cra-cli-plugin#terraform-scc-rules). Controls that are part of the deployable architecture and that are also supported by {{site.data.keyword.cloud_notm}} projects are checked. Any extra controls that are not included in the list of supported {{site.data.keyword.compliance_short}} rules are not checked when you validate the configuration.

        If the validation fails because of the Code Risk Analyzer scan, you can [troubleshoot the failure](/docs/powervs-vpc?topic=powervs-vpc-ts-na-failures).
1.  Deploy the configuration:

    After you validate your configuration, you can deploy it to your target account.

    1.  Review the input values and make any necessary changes.
    1.  Click **Deploy**.

        Deploying the deployable architecture can take more than an hour. You are notified when the deployment is successful.

1.  Review the outputs from the deployable architecture.

During the validation and deployment process, monitor the [needs attention items](/docs/secure-enterprise?topic=secure-enterprise-needs-attention-projects). The widget reflects any issue that occurs in your configurations.
{: remember}

## Next steps
{: #next-with-vsi}

* Connecting to landscape by using [Client to site VPN](/docs/powervs-vpc?topic=powervs-vpc-solution-connect-client-vpn)
* Connecting to landscape by using [Floating IP](/docs/powervs-vpc?topic=powervs-vpc-solution-ssh)
