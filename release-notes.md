---

copyright:
  years: 2023, 2024
lastupdated: "2024-03-21"

keywords: 

subcollection: powervs-vpc

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture
{: #powervs-vpc-relnotes}

Use these release notes to learn about the latest updates to the {{site.data.keyword.powerSys_notm}} with VPC landing zone. The entries grouped by date.
{: shortdesc}

## 21 March 2024
{: #powervs-vpc-mar21}
{: release-note}

Version 4.6.1 of the available
: Version 4.6.1 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Upgrade Tokyo 04 `tok04` DC to PER. New deployments in Tokyo region will make use of PER.

[Warning]{: tag-red}
: Version 4.6.1 includes backward-incompatible changes for Tokyo 04 `tok04` DC only. 
    - Do not upgrade to this version if previous deployments were made in Tokyo 04 `tok04` {{site.data.keyword.powerSys_notm}} zone as doing so will corrupt the landscape because of switch from Cloud connections to PER.
    - Use this for new deployments in Tokyo 04 `tok04` {{site.data.keyword.powerSys_notm}} zone.
    - Deployments done in other {{site.data.keyword.powerSys_notm}} zone can be upgraded with any issue.

## 7 February 2024
{: #powervs-vpc-feb7}
{: release-note}

Version 4.5.0 of the available
: Version 4.5.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Upgrade Sao Paulo 01 `sao01` DC to PER. New deployments in Sao Paulo 01 region will make use of PER.

[Warning]{: tag-red}
: Version 4.5.0 includes backward-incompatible changes for Sao Paulo 01 `sao01` DC only. 
    - Do not upgrade to this version if previous deployments were made in Sao Paulo 01 `sao01` {{site.data.keyword.powerSys_notm}} zone as doing so will corrupt the landscape because of switch from Cloud connections to PER.
    - Use this for new deployments in Sao Paulo 01 `sao01` {{site.data.keyword.powerSys_notm}} zone.
    - Deployments done in other {{site.data.keyword.powerSys_notm}} zone can be upgraded with any issue.

## 1 February 2024
{: #powervs-vpc-feb1}
{: release-note}

Version 4.4.0 of the available
: Version 4.4.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Upgrade Dallas 12 `dal12` DC to PER. New deployments in Dallas 12 region will make use of PER.

[Warning]{: tag-red}
: Version 4.4.0 includes backward-incompatible changes for Dallas 12 `dal12` DC only. 
    - Do not upgrade to this version if previous deployments were made in Dallas 12 `dal12` {{site.data.keyword.powerSys_notm}} zone as doing so will corrupt the landscape because of switch from Cloud connections to PER.
    - Use this for new deployments in Dallas 12 `dal12` {{site.data.keyword.powerSys_notm}} zone.
    - Deployments done in other {{site.data.keyword.powerSys_notm}} zone can be upgraded with any issue.

## 22 January 2024
{: #powervs-vpc-jan22}
{: release-note}

Version 4.3.0 of the available
:   Version 4.3.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Introducing the new import-workspace variant of {{site.data.keyword.powerSys_notm}} with VPC landing zone deployable architecture. See [{{site.data.keyword.powerSys_notm}} with VPC landing zone import-workspace variation](https://cloud.ibm.com/docs/powervs-vpc?topic=powervs-vpc-powervs-automation-overview#overview-powervs-workspace-import-variant) for more information.

## 11 January 2024
{: #powervs-vpc-jan11}
{: release-note}

Version 4.2.0 of the available
:   Version 4.2.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Upgrade Frankfurt 1 `eu-de-1` DC to PER. New deployments in Frankfurt 1 region will make use of PER.

[Warning]{: tag-red}
: Version 4.2.0 includes backward-incompatible changes for Frankfurt 1 `eu-de-1` DC only . 
    - Do not upgrade to this version if previous deployments were made in Frankfurt 1 `eu-de-1` {{site.data.keyword.powerSys_notm}} zone as doing so will corrupt the landscape because of switch from Cloud connections to PER.
    - Use this for new deployments in Frankfurt 1 `eu-de-1` {{site.data.keyword.powerSys_notm}} zone.
    - Deployments done in other {{site.data.keyword.powerSys_notm}} zone can be upgraded with any issue.

## 10 January 2024
{: #powervs-vpc-jan10}
{: release-note}

Version 4.1.0 of the available
:   Version 4.1.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Enable support for `WDC07`, `MAD02`, `MAD04` and `SAO04` PER datacenters for {{site.data.keyword.powerSys_notm}} Workspace Variation only.
    - Enable support for `WDC07`and `SAO04`  PER datacenters for {{site.data.keyword.powerSys_notm}} Quickstart Variation.
    - Upgrade Frankfurt 2 `eu-de-2` DC to PER. New deployments in Frankfurt 2 region will make use of PER.
    - Fixes outputs of workspace when DNS, NTP and NFS services are set to false.

[Warning]{: tag-red}
: Version 4.1.0 includes backward-incompatible changes for Frankfurt 2 `eu-de-2` DC only . 
    - Do not upgrade to this version if previous deployments were made in Frankfurt 2 `eu-de-2` {{site.data.keyword.powerSys_notm}} zone as doing so will corrupt the landscape because of switch from Cloud connections to PER.
    - Use this for new deployments in Frankfurt 2 `eu-de-2` {{site.data.keyword.powerSys_notm}} zone.
    - Deployments done in other {{site.data.keyword.powerSys_notm}} zone can be upgraded with any issue.

## 08 January 2024
{: #powervs-vpc-jan08}
{: release-note}

Version 4.0.1 of the available
:   Version 4.0.1 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Upgrade TF IBM provider version to `1.61.0`
    - Change default PowerVS images for AIX and IBM i for all variations
    - Quickstart flavour now has a tshirt size `Custom (Configure in optional parameters)` in the dropdown. This is used when `custom_profile` needs to be used for custom deployments.

[Breaking change]{: tag-red}
: Version 4.0.1 includes backward-incompatible changes. Review the following information before you upgrade.
    - When upgrading to this version floating IPs are going to be deleted and recreated upon apply. This is due to a bug where the floating IPs were being created incorrectly in the Default resource group. Upon re-creation, the floating IPs will be created in the same resource group as the VSI.
    - Please plan accordingly before upgrading incase this change will cause disruption for whatever is using the floating IPs.
    - 3 sleep resources will be deleted because of changes in the VPC landing zone module version 

## 05 December 2023
{: #powervs-vpc-dec05}
{: release-note}

Version 3.2.0 of the available
:   Version 3.2.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Support `MAD02` data center which is [PER enabled](/docs/power-iaas?topic=power-iaas-per).

## 22 November 2023
{: #powervs-vpc-nov22}
{: release-note}

Version 3.1.0 of the available
:   Version 3.1.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Support `WDC06` data center which is [PER enabled](/docs/power-iaas?topic=power-iaas-per).

## 27 October 2023
{: #powervs-vpc-oct27}
{: release-note}

Version 3.0.0 of the available
:   Version 3.0.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Support all private {{site.data.keyword.powerSys_notm}} CIDRs in ACL rule.
    - Import any number of {{site.data.keyword.powerSys_notm}} images, and in parallel.
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
{: #powervs-vpc-sep06}
{: release-note}

Version 2.0.0 available
:   Version 2.0.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Support RHEL 8.6 and SLES 15.4 images
    - Support `DAL10` data center which is [PER enabled](/docs/power-iaas?topic=power-iaas-per).

## 23 August 2023
{: #powervs-vpc-aug23}
{: release-note}

Version 1.2.0 available
:   Version 1.2.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Introducing the new quickstart variant of {{site.data.keyword.powerSys_notm}} with VPC landing zone deployable architecture. See [{{site.data.keyword.powerSys_notm}} with VPC landing zone quickstart variation](https://cloud.ibm.com/docs/powervs-vpc?topic=powervs-vpc-powervs-automation-overview#overview-powervs-quickstart-variant) for more information.

## 06 July 2023
{: #powervs-vpc-jul06}
{: release-note}

Version 1.1.0 available
:   Version 1.1.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Introducing {{site.data.keyword.powerSys_notm}} with VPC landing zone
    - The {{site.data.keyword.powerSys_notm}} with VPC landing zone deployable architecture is released. You can use the deployable architecture to create an isolated PowerVS landscape connected with VPC landing zone.
