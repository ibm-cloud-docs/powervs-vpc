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
{: #powervs-vpc-oct27}
{: release-note}

Version 3.0.0 of the available
:   Version 3.0.0 of the Power Virtual Server with VPC landing zone deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Support all private Power Virtual Server CIDRs in ACL rule.
    - Import any number of Power Virtual Server images, and in parallel.
    - The `clean_default_sg_acl` input is included in the landing zone preset to clean the default sg rule for new deployments.
    - Upgrade to `ibm-sles-15-4-amd64-sap-applications-6` & `ibm-redhat-8-6-amd64-sap-applications-4` on intel VSI landing zone for new deployments. This does not affect the previous DA version.

[Breaking change]{: tag-red}
: Version 3.0.0 includes backward-incompatible changes. Review the following information before you upgrade.
    - Back up the data on the 10.20.10.4 `private-svs-1` VSI in the `/nfs` directory before you upgrade to version 3.0.0.
    - When you upgrade the full-stack solution, the Ansible roles are triggered again, the ACL rules are updated, and the NFS disk will be re-created.
    - Schedule the upgrade. 
        - The new landing zone version re-creates the 1 TB storage disk in a different resource group, so you will experience down time.
        - When you upgrade, the deployable architecture will be down for about 20 minutes, and the Intel VSI will reboot.
   - If you deployed the QuickStart variation, you might want to create another deployable architecture rather than upgrade. The VM and VPC subnets are re-created, which might affect demos and PoCs.

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
