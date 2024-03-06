---

copyright:
  years: 2023
lastupdated: "2023-11-03"

keywords:

subcollection: powervs-vpc

---

{{site.data.keyword.attribute-definition-list}}

# Before you begin deploying the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture
{: #powervs-automation-planning}

Before you begin the deployment, ensure that the prerequisites for the deployable architecture are met.
{: shortdesc}

## Confirm your {{site.data.keyword.cloud_notm}} settings
{: #vpc-cloud-prereqs}

Complete the following steps before you deploy the {{site.data.keyword.powerSys_notm}} with VPC landing zone deployable architecture.

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

## Create an SSH key Pair
{: #powervs-automation-ssh-key}

Make sure that you have an SSH key that you can use for authentication. This key is used to log in to all virtual server instances that you create. For more information about creating SSH keys, see [SSH keys](/docs/vpc?topic=vpc-ssh-keys).

SSH Key can be generated using any methods. When generating a key pair, make sure the passphrase is empty(must not be password encrypted).

### Linux OS:
On the command line type the command `ssh-keygen`. It will place the id_rsa and id_rsa.pub files under `/root/.ssh/id_rsa`.

```sh
ssh-keygen
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

### Windows OS:
You can install [MobaXterm](https://mobaxterm.mobatek.net/download.html) application and start a local terminal.
On the command line type the command `ssh-keygen`. It will place the id_rsa and id_rsa.pub files under `/home/mobaxterm/.ssh/`

```sh
ssh-keygen
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

Paste the content of `id_rsa.pub` key directly in the field for input variable `ssh_public_key`.
For `ssh_private_key` input variable, you need a [here-doc](https://developer.hashicorp.com/terraform/language/expressions/strings#heredoc-strings) string format.
Replace value with your private ssh key value. You can use a text editor. Then copy the entire content and paste it in the field for `ssh_private_key` input variable.

```sh
<<-EOF
-----BEGIN RSA PRIVATE KEY-----
value
-----BEGIN RSA PRIVATE KEY-----
EOF

```

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
| Management VPC | VPC management network for virtual server instances  | 10.10.10.0/24 |
| Workload VPC | VPC workload network for virtual server instances | 10.20.10.0/"4 |
| Edge VPC | VPC edge network for virtual server instances | 10.30.10.0/24 |
| Power VS workspace | Power VS management network  \n PowerVS backup network  | 10.51.0.0/24 \n 10.52.0.0/24 |
{: caption="Table 1. Private networks IP address ranges" caption-side="bottom"}

## Learn about deployment input parameters
{: #powervs-automation-input-parameters}

Ensure that you are familiar with the required input for the deployment execution. 
- [Description for 'Fullstack' input parameters - create new architecture](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure/blob/main/solutions/full-stack/README.md){: external}
- [Description for 'Extension' input parameters - extend existing architecture](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure/blob/main/solutions/extension/README.md){: external}
- [Description for 'Quickstart' input parameters - create new architecture](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure/blob/main/solutions/quickstart/README.md){: external}

## Additional background information
{: #power-automation-prereqs-additional}

- [{{site.data.keyword.powerSys_notm}} service documentation](https://cloud.ibm.com/docs/power-iaas)
- [Deployable architecture code](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure){: external}
- Main dependencies:
   - [https://github.com/terraform-ibm-modules/terraform-ibm-landing-zone](https://github.com/terraform-ibm-modules/terraform-ibm-landing-zone){: external}
   - [https://galaxy.ansible.com/ibm/power_linux_sap](https://galaxy.ansible.com/ibm/power_linux_sap){: external}
   