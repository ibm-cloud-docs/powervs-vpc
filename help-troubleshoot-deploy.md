---

copyright:
  years: 2023, 2024
lastupdated: "2024-09-23"

keywords:

subcollection: powervs-vpc

---

{{site.data.keyword.attribute-definition-list}}

# My deployment failed, how do I proceed?
{: #troubleshoot-deploy}
{: troubleshoot}

Your deployment failed.
{: shortdesc}

You attempted to deploy a variation of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture but it failed.
{: tsSymptoms}

Several infrastructure layers and components are included in the deployment, and an issue in one of those pieces is causing the failure. For example, maintenance in a particular data center or errors in the VPC or network services can cause deployment failures.
{: tsCauses}

If the deployment process does not finish successfully, look at the {{site.data.keyword.bplong_notm}} logs. These logs typically provide the information about the component that causes the issue.

If you can't deploy successfully, follow these steps:

1.  Make sure that you comply with the prerequisites in the [planning](/docs/powervs-vpc?topic=powervs-vpc-plan)
1.  Check the values of the inputs.
    For example, from the **Configurations** tab in your project, click the name of your deployable architecture > **Edit**.
1.  Rerun the Deployment action again in {{site.data.keyword.bplong_notm}} by clicking **Deploy again**.

This action resumes the job where it left off. In some cases, when the error was with provisioning a service, this second apply command is successful.

If the issue persists after the second apply, [open a case](/docs/powervs-vpc?topic=powervs-vpc-help-support#support-case-details) in the {{site.data.keyword.cloud_notm}} support center.
{: tsResolve}
