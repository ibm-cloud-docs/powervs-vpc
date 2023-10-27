---

copyright:
  years: 2023
lastupdated: "2023-10-27"

keywords: 

subcollection: powervs-vpc

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for the Power Virtual Server with VPC landing zone deployable architecture
{: #powervs-vpc-relnotes}

Use these release notes to learn about the latest updates to the Power Virtual Server with VPC landing zone. The entries grouped by date.
{: shortdesc}

## 27 October 2023
{: #powervs-vpc-oct23}
{: release-note}

New product version `V3.0.0` introduced. The new product version supports the following:
- Support all private {{site.data.keyword.powerSys_notm}} CIDRs in ACL rule.
- Import any number of {{site.data.keyword.powerSys_notm}} images and in parallel.
- `Clean_default_sg_acl` included in the landing zone preset to clean the default sg rule for new deployments.
- Upgrade to `ibm-sles-15-4-amd64-sap-applications-6` & `ibm-redhat-8-6-amd64-sap-applications-4` on intel VSI landing zone for new deployments. This will not affect the previous DA version.
- All DAs now use *terraform-ibm-modules/powervs-workspace/ibm* module to create {{site.data.keyword.powerSys_notm}} Workspace.
- Change name of data center in drop down for DAs and make it more detailed for Power Edge Router (PER).
- Upgrade ibm provider to `1.58.1` for all DA soltuions.
- Expose NFS disk configuration and now it is optional. Size and mount path of volume can be specified.
- Faster parallel deployments of landing zone and {{site.data.keyword.powerSys_notm}} infrastructure.
- **Fix**: DNS settings on landing zone vsi (upgraded to 1.1.4 version ansible collection ibm.power_linux_sap collection).

Breaking Change:
- Please backup the data on 10.20.10.4 private-svs-1 vsi under the /nfs directory before upgrading to this.
DAs will be affected with recreating the 1TB storage disk as the new landing zone version will recreate the disk in correct resource group. :warning: There will be down time :warning: if upgrading the fullstack stack solution. All the ansible roles will be triggered again, acl rules will be updated and the nfs disk will be back.
- When upgrading there will be downtime for about 20 mins, reboots of intel vsi will be made.
- Not recommend to upgrade Quickstart Version as it recreates a VM, VPC subnets,  as this solution is purely for demo purposes and PoCs.
{: warning}

## 06 September 2023
{: #powervs-vpc-sep23}
{: release-note}

New product version `V2.0.0` introduced. The new product version supports the following:
- IBM i 7.5
- `DAL10` data center which is [PER enabled](/docs/power-iaas?topic=power-iaas-per).

## 22 August 2023
{: #powervs-vpc-aug23}
{: release-note}

Introducing the new quickstart variant of Power Virtual Server with VPC landing zone deployable architecture. See [Power Virtual Server with VPC landing zone quickstart variation](https://test.cloud.ibm.com/docs/powervs-vpc?topic=powervs-vpc-powervs-automation-overview##qkstart-variant) for more information.

## 30 April 2023
{: #powervs-vpc-apr0430}
{: release-note}

Introducing Power Virtual Server with VPC landing zone
:   The Power Virtual Server with VPC landing zone deployable architecture is released. You can use the deployable architecture to create an isolated PowerVS landscape connected with VPC landing zone.
