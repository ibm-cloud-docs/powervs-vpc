---

copyright:
  years: 2023
lastupdated: "2023-04-06"

keywords:

subcollection: powervs-vpc

---

{{site.data.keyword.attribute-definition-list}}

# Getting help and support for {{site.data.keyword.powerSysFull}} with VPC landing zone
{: #powervs-automation-solution-support}

If you experience an issue or have questions when deploying {{site.data.keyword.powerSys_notm}} with VPC landing zone, you can use the following resources before you open a support case.
{: shortdesc}

- Review the [FAQs](/docs/powervs-vpc?topic=powervs-vpc-powervs-automation-faqs) in the deployment guide.
- Review the [troubleshooting documentation](/docs/powervs-vpc?topic=powervs-vpc-troubleshoot-deploy) to troubleshoot and resolve common issues.
- ![GitHub icon](../icons/logo-github-16.svg "GitHub icon") Review the [GitHub issues](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure/issues){: external} to see whether other users experienced the same problem.
- ![Slack icon](../icons/logo-slack-16.svg "Slack icon") Ask product experts and the community questions on the [sap-on-power-deployable-architectures](https://ibm-cloudplatform.slack.com/archives/C04RJB1UX53) Slack channel.

If you still can't resolve the problem, you can open a support case. For more information, see [Creating support cases](/docs/get-support?topic=get-support-open-case). And, if you're looking to provide feedback, see [Submitting feedback](/docs/overview?topic=overview-feedback).

## Providing support case details
{: #powervs-automation-support-case-details}

To ensure that the support team can start investigating your case to provide a timely resolution, you must include the architecture name, source URL, and version from your Schematics log.

1. In the {{site.data.keyword.cloud_notm}} console, go to **Schematics** > **Workspaces** > **deployable architecture instance**.
1. Copy and paste into the case details the portion of the log that provides the architecture information. The following is an example of what should be copied:

   ```sh
   023/04/13 20:50:40 Related Workspace: name=auto-test-infra-osa21-13-04-2023, sourcerelease=(not specified), sourceurl=https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure/archive/v6.2.0.tar.gz, folder=terraform-ibm-powervs-infrastructure-6.2.0/examples/ibm-catalog/deployable-architectures/full-stack
   ```

## Routing your support case expeditiously 
{: #powervs-automation-support-case-routing}

To get your support case routed correctly to speed up resolution, make sure that you select the right product when you open the case. 

If you're having issues getting the deployable architecture deployed, use the name of the deployable architecture as it is listed in the catalog. 

However, if you successfully deployed and are instead having an issue with a service (for example, PowerVS or VPC service) in the deployable architecture, set that service as the product name in the case. 
