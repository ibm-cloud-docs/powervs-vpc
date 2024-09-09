---

copyright:
  years: 2023, 2024
lastupdated: "2024-09-09"

keywords:

subcollection: powervs-vpc

---

{{site.data.keyword.attribute-definition-list}}

# Planning for the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture
{: #plan}

Before you begin the deployment, make sure that you understand and meet the prerequisites.
{: shortdesc}

## Confirm your {{site.data.keyword.cloud_notm}} settings
{: #powervs-automation-cloud-prereqs}

Complete the following steps before you deploy the {{site.data.keyword.powerSys_notm}} with VPC landing zone deployable architecture.

1.  Confirm or set up an {{site.data.keyword.cloud_notm}} account:

    Make sure that you have an {{site.data.keyword.cloud_notm}} Pay-As-You-Go or Subscription account:

    - If you don't have an {{site.data.keyword.cloud_notm}} account, [create one](/docs/account?topic=account-account-getting-started).
    - If you have a Trial or Lite account, [upgrade your account](/docs/account?topic=account-upgrading-account).
1.  Configure your {{site.data.keyword.cloud_notm}} account:
    1.  Log in to [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com) with the {{site.data.keyword.ibmid}} you used to set up the account. This {{site.data.keyword.ibmid}} user is the account owner and has full IAM access.
    1.  [Complete the company profile](/docs/account?topic=account-contact-info) and contact information for the account. This profile is required to stay in compliance with {{site.data.keyword.cloud_notm}} Financial Services profile.
    1.  [Enable the Financial Services Validated option](/docs/account?topic=account-enabling-fs-validated) for your account.
    1.  Enable virtual routing and forwarding (VRF) and service endpoints by creating a support case. Follow the instructions in [enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint&interface=ui#vrf).

## Set the IAM permissions
{: #powervs-automation-IAM-prereqs}

1.  Set up account access ({{site.data.keyword.iamshort}} (IAM)):
    1.  Create an {{site.data.keyword.cloud_notm}} [API key](/docs/account?topic=account-userapikey&interface=terraform#create_user_key-api-terra). The user who owns this key must have the Administrator role.

        Service ID API keys are not supported for the Red Hat OpenShift Container Platform on VPC landing zone deployable architecture.
        {: tip}

    1.  For compliance with {{site.data.keyword.framework-fs_notm}}: Require users in your account to use [multifactor authentication (MFA)](/docs/account?topic=account-account-getting-started#account-gs-mfa).
    1.  [Set up access groups](/docs/account?topic=account-account-getting-started#account-gs-accessgroups).

        User access to {{site.data.keyword.cloud_notm}} resources is controlled by using the access policies that are assigned to access groups. For {{site.data.keyword.cloud_notm}} Financial Services validation, do not assign direct IAM access to any {{site.data.keyword.cloud_notm}} resources.

        Select **All Identity and Access enabled services** when you assign access to the group.

### Verify access roles
{: #powervs-automation-access-roles}

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

You need the following access to create a project and create project tooling resources within the account. Make sure you have the following access:

- The Editor role on the Projects service.
- The Editor and Manager role on the {{site.data.keyword.bpshort}} service
- The Viewer role on the resource group for the project

For more information, see [Assigning users access to projects](/docs/secure-enterprise?topic=secure-enterprise-access-project).

## Create an SSH key Pair
{: #powervs-automation-ssh-key}

Make sure that you have an SSH key that you can use for authentication. This key is used to log in to all virtual server instances that you create. For more information about creating SSH keys, see [SSH keys](/docs/vpc?topic=vpc-ssh-keys).

SSH Key can be generated by using any method. When generating a key pair, make sure that the **passphrase is empty(must not be password encrypted)**.

### Linux OS
{: #ssh-key-linux}

On the command line type, the command `ssh-keygen`. It places the id_rsa and id_rsa.pub files under `/root/.ssh/id_rsa`.

```sh
ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /root/.ssh/id_rsa
Your public key has been saved in /root/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:TUdZn9O6tnwK2lc4m917Cs1KvbyXs2n46yrlE2I1t/I root@ans-jump-box-001
The key's randomart image is:
+---[RSA 3072]----+
|            .o.  |
|           ..  .o|
|          . .  oo|
|         o . o o.|
|        S . . +..|
|           o Boo.|
|          . B @*o|
|           = @+EB|
|          . +o#&*|
+----[SHA256]-----+
```

### Windows OS
{: #ssh-key-windows}

You can install [MobaXterm](https://mobaxterm.mobatek.net/download.html){: external} application and start a local terminal.
On the command line type, the command `ssh-keygen`. It places the id_rsa and id_rsa.pub files under `/home/mobaxterm/.ssh/`

```sh
ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/mobaxterm/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/mobaxterm/.ssh/id_rsa
Your public key has been saved in /home/mobaxterm/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:TUdZn9O6tnwK2lc4m917Cs1KvbyXs2n46yrlE2I1t/I
The key's randomart image is:
+---[RSA 3072]----+
|            .o.  |
|           ..  .o|
|          . .  oo|
|         o . o o.|
|        S . . +..|
|           o Boo.|
|          . B @*o|
|           = @+EB|
|          . +o#&*|
+----[SHA256]-----+
```

These public and private keys can now be used in the input variables for the Deployable architectures.

Paste the content of `id_rsa.pub` key and `id_rsa` key directly in the field for input variables `ssh_public_key` and `ssh_private_key`respectively.


## Client to site VPN configuration
{: #powervs-automation-vpn-prereqs}

- The list of users who will connect over the VPN connection to your {{site.data.keyword.cloud_notm}} account.

    The module takes a list of email addresses of the users in your {{site.data.keyword.cloud_notm}} account. For more information about how to add users, see [Inviting users to an account](/docs/account?topic=account-iamuserinv&interface=ui).

- If you have a {{site.data.keyword.secrets-manager_short}} instance, you need the following information:

    The Terraform module creates a {{site.data.keyword.secrets-manager_short}} instance if you don't already have one.
    {: reminder}

    - Copy the `region` of your {{site.data.keyword.secrets-manager_short}} instance by using the {{site.data.keyword.cloud_notm}} console.
    - Copy the `GUID` of the instance. You can locate the {{site.data.keyword.secrets-manager_short}} GUID in your account from the resource list in the {{site.data.keyword.cloud_notm}} console as shown in the following screenshot.
        1.  Enter `secret` in the product filter. A list of {{site.data.keyword.secrets-manager_short}} instances are displayed.
        1.  Click the row to display the details in the sidebar for the {{site.data.keyword.secrets-manager_short}} instance that you want to use.
        1.  Copy the GUID.

            ![Example of resource list](images/secrets-manager-resource-list.png){: caption="Figure 1. Example view of the resource list in {{site.data.keyword.cloud_notm}} console" caption-side="bottom"}
    - If you used a certificate template to create a private certificate that is applied to your {{site.data.keyword.secrets-manager_short}} instance, copy the name of the certificate template.
        1.  In the resource list, click the name of the {{site.data.keyword.secrets-manager_short}} instance that you selected earlier.
        1.  Click **Secrets engines** > **Private certificates**.
        1.  In the Certificate authority table, expand the certificate authority and copy the name of the template.

## Additional background information
{: #power-automation-prereqs-additional}

- [{{site.data.keyword.powerSys_notm}} service documentation](https://cloud.ibm.com/docs/power-iaas)
- [Deployable architecture code](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure){: external}
- Main dependencies:
   - [Terraform IBM Module - VPC Landing Zone](https://github.com/terraform-ibm-modules/terraform-ibm-landing-zone){: external}
   - [Terraform IBM Module - PowerVS Workspace](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-workspace){: external}
   - [Terraform IBM Module - PowerVS Instance](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-instance){: external}
   - [Terraform IBM Module - Client to site VPN](https://github.com/terraform-ibm-modules/terraform-ibm-client-to-site-vpn){: external}
   - [Terraform IBM Module - Secret Manager](https://github.com/terraform-ibm-modules/terraform-ibm-secrets-manager){: external}
   - [Terraform IBM Module - Secrets Manager Group](https://github.com/terraform-ibm-modules/terraform-ibm-secrets-manager-secret-group){: external}
   - [Terraform IBM Module - Private Secret Engine](https://github.com/terraform-ibm-modules/terraform-ibm-secrets-manager-private-cert-engine){: external}
   - [Terraform IBM Module - Secrets Manager Private Certificate](https://github.com/terraform-ibm-modules/terraform-ibm-secrets-manager-private-cert){: external}
   - [IBM Power Linux SAP ansible galaxy role](https://galaxy.ansible.com/ibm/power_linux_sap){: external}
   
