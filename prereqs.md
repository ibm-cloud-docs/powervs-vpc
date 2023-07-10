---

copyright:
  years: 2023
lastupdated: "2023-07-10"

keywords:

subcollection: powervs-vpc

---

{{site.data.keyword.attribute-definition-list}}

# Before you begin deploying the Power Virtual Server with VPC landing zone deployable architecture
{: #powervs-automation-planning}

Before you begin the deployment, ensure that the prerequisites for the deployable architecture are met.
{: shortdesc}

## Confirm your {{site.data.keyword.cloud_notm}} settings
{: #vpc-cloud-prereqs}

Complete the following steps before you deploy the Power Virtual Server with VPC landing zone deployable architecture.

1.  Confirm or set up an {{site.data.keyword.cloud_notm}} account:

    Make sure that you have an {{site.data.keyword.cloud_notm}} Pay-As-You-Go or Subscription account:

    - If you don't have an {{site.data.keyword.cloud_notm}} account, [create one](/docs/account?topic=account-account-getting-started).
    - If you have a Trial or Lite account, [upgrade your account](/docs/account?topic=account-upgrading-account).
1.  Configure your {{site.data.keyword.cloud_notm}} account:
    1.  Log in to [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com){: external} with the {{site.data.keyword.ibmid}} you used to set up the account. This {{site.data.keyword.ibmid}} user is the account owner and has full IAM access.
    1.  [Complete the company profile](/docs/account?topic=account-contact-info) and contact information for the account. This profile is required to stay in compliance with {{site.data.keyword.cloud_notm}} Financial Services profile.
    1.  [Enable the Financial Services Validated option](/docs/account?topic=account-enabling-fs-validated) for your account.
    1.  Enable virtual routing and forwarding (VRF) and service endpoints by creating a support case. Follow the instructions in [enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint&interface=ui#vrf).

## Set the IAM permissions
{: #powervs-automation-IAM-prereqs}

Set up account access ({{site.data.keyword.iamshort}} (IAM)):
- Create an {{site.data.keyword.cloud_notm}} [API key](/docs/account?topic=account-userapikey#create_user_key). The user who owns this key must have the Administrator role.

    Service ID API keys are not supported for the Red Hat OpenShift Container Platform on VPC landing zone deployable architecture.
    {: tip}

- For compliance with {{site.data.keyword.framework-fs_notm}}, users in your account are required to use [multi-factor authentication (MFA)](/docs/account?topic=account-account-getting-started#account-gs-mfa).
- [Set up access groups](/docs/account?topic=account-accoungetting-started#account-gs-accessgroups).

    User access to {{site.data.keyword.cloud_notm}} resources is controlled by using the access policies that are assigned to access groups. For {{site.data.keyword.cloud_notm}} Financial Services validation, do not assign direct IAM access to any {{site.data.keyword.cloud_notm}} resources.

    Select **All Identity and Access enabled services** when you assign access to the group.

### Verify access roles
{: #vpc-access-roles}

IAM access roles are required to install this deployable architecture and create all the required elements.

You need the following permissions for this deployable architecture:

- Create services from {{site.data.keyword.cloud_notm}} catalog.
- Create and modify {{site.data.keyword.vpc_short}} services, virtual server instances, networks, network prefixes, storage volumes, SSH keys, and security groups of this VPC.
- Create and modify {{site.data.keyword.powerSysShort}} services, virtual server instances, networks, storage volumes, ssh keys of this {{site.data.keyword.powerSysShort}}.
- Create and modify {{site.data.keyword.cloud_notm}} direct links and {{site.data.keyword.tg_full_notm}}.
- Access existing {{site.data.keyword.cos_short}} services.

For information about configuring permissions, contact your {{site.data.keyword.cloud_notm}} account administrator.

### Access for {{site.data.keyword.cloud_notm}} projects
{: #access-projects}

You can use {{site.data.keyword.cloud_notm}} projects as a deployment option. Projects are designed with infrastructure as code and compliance in mind to help ensure that your projects are managed, secure, and always compliant. For more information, see [Learn about IaC deployments with projects](/docs/secure-enterprise?topic=secure-enterprise-understanding-projects).

You need the following access to create a project and create project tooling resources within the account. Make sure that you have the following access:

- The Editor role on the Projects service
- The Editor and Manager role on the {{site.data.keyword.bpshort}} service
- The Viewer role on the resource group for the project

For more information, see [Assigning users access to projects](/docs/secure-enterprise?topic=secure-enterprise-access-project).

## Create an SSH key
{: #powervs-automation-ssh-key}

Make sure that you have an SSH key that you can use for authentication. This key is used to log in to all virtual server instances that you create. For more information about creating SSH keys, see [SSH keys](/docs/vpc?topic=vpc-ssh-keys).

## Choose an operating system
{: #powervs-automation-select-os}

Choose a Linux operating system for your deployments. We recommend that you use the same OS release for all the hosts in the environment. When you use the same operating system version and release, it simplifies the operations management of the whole landscape. You might choose between Red Hat Enterprise Linux and Suse Linux Enterprise Server.

## Private networks
{: #powervs-automation-private-networks}

The following table lists the private networks that are created by the deployment automation with corresponding default values. 

The defaults must be changed if you specify more than one deployment landscape connected with each other. All IP address ranges in the subnets must be unique.
{: note}

| Service | Private network | IP address ranges |
| --- | --- | --- |
| Management VPC | VPC management network for virtual server instances  | 172.10.1.0/24 |
| Workload VPC | VPC workload network for virtual server instances | 172.11.2.0/24 |
| Edge VPC | VPC edge network for virtual server instances | 172.11.1.0/24 |
| Power VS workspace | Power VS management network  \n PowerVS backup network  \n  \n Separate network for each SAP system on Power VS | 10.10.10.0/24 \n 10.10.11.0/24 \n 10.10.20.0/24 |
{: caption="Table 1. Private networks IP address ranges" caption-side="bottom"}

## Learn about deployment input parameters
{: #powervs-automation-input-parameters}

Ensure that you are familiar with the required input for the deployment execution. 
- [description for input parameters - create new architecture](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure/blob/main/examples/ibm-catalog/deployable-architectures/full-stack/README.md){: external}
- [description for input parameters - extend existing architecture](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure/blob/main/examples/ibm-catalog/deployable-architectures/extension/README.md){: external}

## Additional background information
{: #power-automation-prereqs-additional}

- [IBM Power Systems Virtual Servers service documentation](https://cloud.ibm.com/docs/power-iaas)
- [Deployable architecture code](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-sap){: external}
- Main dependencies:
   - [https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure){: external}
   - [https://galaxy.ansible.com/ibm/power_linux_sap](https://galaxy.ansible.com/ibm/power_linux_sap){: external}
   - [https://galaxy.ansible.com/community/sap_install](https://galaxy.ansible.com/community/sap_install){: external}
