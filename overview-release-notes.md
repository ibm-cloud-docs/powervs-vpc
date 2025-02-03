---

copyright:
   years: 2023, 2025
lastupdated: "2025-02-03"
keywords:
subcollection: powervs-vpc
content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture
{: #powervs-vpc-relnotes}

Use these release notes to learn about the latest updates to the {{site.data.keyword.powerSys_notm}} with VPC landing zone. The entries are grouped by date.
{: shortdesc}

## January 2025
{: #powervs-vpc-2025-01}

### 24 January 2025
{: #powervs-vpc-jan24}
{: release-note}

Version 8.1.2 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 8.1.2 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}
    - Users can now specify their desired boot image for VPC's Intel Virtual Server Instances
    - Updated the default AiX image for product variation 'standard-plus-vsi'
    - Upgraded IBM provider version to 1.74.0
    
### 07 January 2025
{: #powervs-vpc-jan07}
{: release-note}

Version 8.1.1 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 8.1.1 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}
    
    **Features:**
    - Upgraded version of `powervs-workspace` module to 2.4.0
        - Support tags for networks and images 
        - Upgrade minimum IBM provider version to >=1.71.0
    - Upgraded version of `powervs-instance` module to 2.3.0
        - Support tags for instance and storage
    - Upgraded Default IBMi and RHEL images for Quickstart 


## December 2024
{: #powervs-vpc-2024-12}

### 13 December 2024
{: #powervs-vpc-dec13}
{: release-note}

Version 8.1.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 8.1.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}
    
    - **Breaking Change**:
        - New landing zone version `6.4.0` creates VSis using `VNIs` and legacy interfaces are not used any more.
        - Landing zone preset reworked to create security groups separately and then assign to VSIs. This will recreate the VSIs.

    **Features:**
    - Provision Monitoring Instance and an intel VSI to host and process monitoring metrics for SAP
    - Upgrade Rhel images running on Intel VSI (jump box and network services vsi to `RHEL 9.4`)
    - Upgraded minimum IBM power linux sap ansible role version to `v3.0.0`
    - Upgraded IBM TF version to `1.71.3`
    - Remove ansible collection version dependencies from scripts instead install collection dependencies from ansible galaxy requirements.yml
    - Support `DAL14` and `LON04` DC
    - Support `Mad04` DC for Quickstart. Deployments in MAD04 requires value in custom profile to be set as this DC supports P10 only.


## November 2024
{: #powervs-vpc-2024-11}

### 20 November 2024
{: #powervs-vpc-nov20}
{: release-note}

Version 7.1.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 7.1.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}
    
    - Upgraded minimum required terraform version to >=1.9.0
    - Upgraded IBM terraform provider version to v1.71.1
    - Upgraded Default IBMi and AIX images for Quickstart
    - Upgraded version of `powervs-workspace` module to 2.2.0
    - support custom image import from Cloud Object Storage to PowerVS workspace for up to three images in the Standard and standard extension variations

### 01 November 2024
{: #powervs-vpc-nov01}
{: release-note}

Version 7.0.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 7.0.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}
    
    - **BREAKING CHANGE:**
        - Version 7.0.0 includes backward-incompatible changes.
        - When you upgrade to version 7.0.0, you might see some of your infrastructure marked for deletion and re-creation. Fully supported migration steps will be available shortly to prevent this from occurring, so if re-creating infrastructure is going to impact day-to-day operations, don't update to this version until there is a fully supported migration path.
    - VPC landing zone deployable architecture is not affected.
    - Allows user to specify the compute profile (cores and memory) for network services Intel VSI
    - The IBM Terraform provider version is now locked to 1.69.2.
    - The `landing-zone-vsi` submodule is updated from 3.3.0 to 4.2.0. In this version, the naming convention for Virtual Server Instances has changed to be `prefix- + the last 4 digits of the subnet ID + a sequential number for each subnet`. For example, `prefix-3ad7-001`.

## July 2024
{: #powervs-vpc-2024-07}

### 29 July 2024
{: #powervs-vpc-jul29}
{: release-note}

Version 6.0.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 6.0.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}

    - **BREAKING CHANGE:**
        - Version 6.0.0 includes backward-incompatible changes.
        - create ibm_is_share in correct resource group and update ansible role version
        - Backup your data. All data on the NFS share will be lost.
        - If you upgrade from an older version, this will destroy and recreate the NFS share in correct resource group. It is important to backup your data. You can copy the the data to COS or copy it locally using commands. The automation does not help in doing this. Once it is recreated and mounted, you can copy the files to the NFS mount.
      

### 03 July 2024
{: #powervs-vpc-jul03}
{: release-note}

Version 5.3.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 5.3.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}
    - Enable support for global transit gateway in optional parameters for standard variation.

## June 2024
{: #powervs-vpc-2024-06}

### 07 June 2024
{: #powervs-vpc-jun07}
{: release-note}

Version 5.2.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 5.2.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}
    - Renamed {{site.data.keyword.powerSys_notm}} Workspace Variation to Standard.
    - Renamed Import {{site.data.keyword.powerSys_notm}} Workspace to Import.

## May 2024
{: #powervs-vpc-2024-05}

### 29 May 2024
{: #powervs-vpc-may29}
{: release-note}

Version 5.1.3 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 5.1.3 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}
    - Take a look at may26 release notes( version 5.1.2).
    - Support Linux images in custom images for Quickstart variation.
    - Upgrade IBMi images in tshirt sizes.


### 26 May 2024
{: #powervs-vpc-may26}
{: release-note}

Version 5.1.2 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 5.1.2 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Completely New architecture. Does not support the upgrade process from previous version  4.x.x to 5.x.x
    - Use this version for new deployments only.
    - Option to create `new secrets manager instance` or reuse existing one.
    - Optional `client to site VPN` deployment.
    - Switched from Block storage NFS volumes to File storage shares. Uses Application Load Balancer to mount the File Storage shares on {{site.data.keyword.powerSys_notm}} instances.
    - Removed Cloud connection support.
    - Private SSH keys need not be entered in here doc string format. Can be passed in directly.
    - Improved documentation.
    - Network-services vsi is now the central ansible execution node.
    - Both intel VSIs run on RHEL 8.8 OS.

[Breaking change]{: tag-red}
: Version 5.1.2 includes backward-incompatible changes.
    - Do not upgrade if you already have an existing deployment.
    - Make a new deployment and then restore your OS data that use data migration techniques.


### 10 May 2024
{: #powervs-vpc-may10}
{: release-note}

Version 4.11.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 4.11.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Upgrade Toronto 01 `tor01` DC to PER. New deployments in theToronto 01 region makes use of PER.
    - Upgrade US-south `us-south` DC to PER. New deployments in theUs-south region makes use of PER.
    - Quickstart now supports SLES SAP DEV t-shirt size.

[Warning]{: tag-red}
: Version 4.11.0 includes backward-incompatible changes for `tor01` and `us-south` DCs only.
    - Do not upgrade to this version if previous deployments were made in `tor01` and `us-south` {{site.data.keyword.powerSys_notm}} zone as doing so corrupts the landscape due to the switch from Cloud Connections to PER.
    - Use this version for New deployments in the`tor01` and `us-south` {{site.data.keyword.powerSys_notm}} zone.
    - Deployments that are done in other {{site.data.keyword.powerSys_notm}} zone can be upgraded with any issue.

## April 2024
{: #powervs-vpc-2024-04}

### 30 April 2024
{: #powervs-vpc-apr30}
{: release-note}

Version 4.10.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 4.10.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Upgrade Sydney 04 `syd04` DC to PER. New deployments in theSydney 04 region makes use of PER.

[Warning]{: tag-red}
: Version 4.10.0 includes backward-incompatible changes for Sydney 04 `syd04` DC only.
    - Do not upgrade to this version if previous deployments were made in Sydney 04 `syd04` {{site.data.keyword.powerSys_notm}} zone as doing so corrupts the landscape due to the switch from Cloud Connections to PER.
    - Use this version for New deployments in theSydney 04 `syd04` {{site.data.keyword.powerSys_notm}} zone.
    - Deployments that are done in other {{site.data.keyword.powerSys_notm}} zone can be upgraded with any issue.

### 14 April 2024
{: #powervs-vpc-apr14}
{: release-note}

Version 4.9.1 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 4.9.1 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Upgrade DAs to version 1.64.1 terraform IBM provider version
    - Upgrade Quickstart Solution to utilize the latest AIX and IBMi images.

### 05 April 2024
{: #powervs-vpc-apr05}
{: release-note}

Version 4.9.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 4.9.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Upgrade London 06 `lon06` DC to PER. New deployments in theLondon 06 region makes use of PER.

[Warning]{: tag-red}
: Version 4.9.0 includes backward-incompatible changes for London 06 `lon06` DC only.
    - Do not upgrade to this version if previous deployments were made in London 06 `lon06` {{site.data.keyword.powerSys_notm}} zone as doing so corrupts the landscape due to the switch from Cloud Connections to PER.
    - Use this version for New deployments in theLondon 06 `lon06` {{site.data.keyword.powerSys_notm}} zone.
    - Deployments that are done in other {{site.data.keyword.powerSys_notm}} zone can be upgraded with any issue.

### 03 April 2024
{: #powervs-vpc-apr03}
{: release-note}

Version 4.8.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 4.8.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Upgrade Sydney 05 `syd05` DC to PER. New deployments in theSydney 05 region makes use of PER.

[Warning]{: tag-red}
: Version 4.8.0 includes backward-incompatible changes for Sydney 05 `syd05` DC only.
    - Do not upgrade to this version if previous deployments were made in Sydney 05 `syd05` {{site.data.keyword.powerSys_notm}} zone as doing so corrupts the landscape due to the switch from Cloud Connections to PER.
    - Use this version for New deployments in theSydney 05 `syd05` {{site.data.keyword.powerSys_notm}} zone.
    - Deployments that are done in other {{site.data.keyword.powerSys_notm}} zone can be upgraded with any issue.

## March 2024
{: #powervs-vpc-2024-03}

### 26 March 2024
{: #powervs-vpc-mar26}
{: release-note}

Version 4.7.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 4.7.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Upgrade Osaka 21 `osa21` DC to PER. New deployments in theOsaka region makes use of PER.

[Warning]{: tag-red}
: Version 4.7.0 includes backward-incompatible changes for Osaka 21 `osa21` DC only.
    - Do not upgrade to this version if previous deployments were made in Osaka 21 `osa21` {{site.data.keyword.powerSys_notm}} zone as doing so corrupts the landscape due to the switch from Cloud Connections to PER.
    - Use this version for New deployments in theOsaka 21 `osa21` {{site.data.keyword.powerSys_notm}} zone.
    - Deployments that are done in other {{site.data.keyword.powerSys_notm}} zone can be upgraded with any issue.

### 21 March 2024
{: #powervs-vpc-mar21}
{: release-note}

Version 4.6.1 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 4.6.1 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Upgrade Tokyo 04 `tok04` DC to PER. New deployments in theTokyo region makes use of PER.

[Warning]{: tag-red}
: Version 4.6.1 includes backward-incompatible changes for Tokyo 04 `tok04` DC only.
    - Do not upgrade to this version if previous deployments were made in Tokyo 04 `tok04` {{site.data.keyword.powerSys_notm}} zone as doing so corrupts the landscape due to the switch from Cloud Connections to PER.
    - Use this version for New deployments in theTokyo 04 `tok04` {{site.data.keyword.powerSys_notm}} zone.
    - Deployments that are done in other {{site.data.keyword.powerSys_notm}} zone can be upgraded with any issue.

## February 2024
{: #powervs-vpc-2024-02}

### 7 February 2024
{: #powervs-vpc-feb7}
{: release-note}

Version 4.5.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 4.5.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Upgrade Sao Paulo 01 `sao01` DC to PER. New deployments in the Sao Paulo 01 region makes use of PER.

[Warning]{: tag-red}
: Version 4.5.0 includes backward-incompatible changes for Sao Paulo 01 `sao01` DC only.
    - Do not upgrade to this version if previous deployments were made in Sao Paulo 01 `sao01` {{site.data.keyword.powerSys_notm}} zone as doing so corrupts the landscape due to the switch from Cloud Connections to PER.
    - Use this version for New deployments in the Sao Paulo 01 `sao01` {{site.data.keyword.powerSys_notm}} zone.
    - Deployments that are done in other {{site.data.keyword.powerSys_notm}} zone can be upgraded with any issue.

### 1 February 2024
{: #powervs-vpc-feb1}
{: release-note}

Version 4.4.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
: Version 4.4.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Upgrade Dallas 12 `dal12` DC to PER. New deployments in the Dallas 12 region makes use of PER.

[Warning]{: tag-red}
: Version 4.4.0 includes backward-incompatible changes for Dallas 12 `dal12` DC only.
    - Do not upgrade to this version if previous deployments were made in Dallas 12 `dal12` {{site.data.keyword.powerSys_notm}} zone as doing so corrupts the landscape due to the switch from Cloud Connections to PER.
    - Use this version for New deployments in the Dallas 12 `dal12` {{site.data.keyword.powerSys_notm}} zone.
    - Deployments that are done in other {{site.data.keyword.powerSys_notm}} zone can be upgraded with any issue.

## January 2024
{: #powervs-vpc-2024-01}

### 22 January 2024
{: #powervs-vpc-jan22}
{: release-note}

Version 4.3.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
:   Version 4.3.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Introducing the new import-workspace variant of {{site.data.keyword.powerSys_notm}} with VPC landing zone deployable architecture. For more information see the [{{site.data.keyword.powerSys_notm}} with VPC landing zone import-workspace variation](/docs/powervs-vpc?topic=powervs-vpc-automation-solution-overview#overview-powervs-workspace-import-variant).

### 11 January 2024
{: #powervs-vpc-jan11}
{: release-note}

Version 4.2.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
:   Version 4.2.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Upgrade Frankfurt 1 `eu-de-1` DC to PER. New deployments in the Frankfurt 1 region makes use of PER.

[Warning]{: tag-red}
: Version 4.2.0 includes backward-incompatible changes for Frankfurt 1 `eu-de-1` DC only .
    - Do not upgrade to this version if previous deployments were made in Frankfurt 1 `eu-de-1` {{site.data.keyword.powerSys_notm}} zone as doing so corrupts the landscape due to the switch from Cloud Connections to PER.
    - Use this version for New deployments in the Frankfurt 1 `eu-de-1` {{site.data.keyword.powerSys_notm}} zone.
    - Deployments that are done in other {{site.data.keyword.powerSys_notm}} zone can be upgraded with any issue.

### 10 January 2024
{: #powervs-vpc-jan10}
{: release-note}

Version 4.1.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
:   Version 4.1.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Enable support for `WDC07`, `MAD02`, `MAD04` and `SAO04` PER datacenters for {{site.data.keyword.powerSys_notm}} Workspace Variation only.
    - Enable support for `WDC07`and `SAO04`  PER datacenters for {{site.data.keyword.powerSys_notm}} Quickstart Variation.
    - Upgrade Frankfurt 2 `eu-de-2` DC to PER. New deployments in the Frankfurt 2 region makes use of PER.
    - Fixes outputs of workspace when DNS, NTP and NFS services are set to false.

[Warning]{: tag-red}
: Version 4.1.0 includes backward-incompatible changes for Frankfurt 2 `eu-de-2` DC only .
    - Do not upgrade to this version if previous deployments were made in Frankfurt 2 `eu-de-2` {{site.data.keyword.powerSys_notm}} zone as doing so corrupts the landscape due to the switch from Cloud Connections to PER.
    - Use this version for New deployments in the Frankfurt 2 `eu-de-2` {{site.data.keyword.powerSys_notm}} zone.
    - Deployments that are done in other {{site.data.keyword.powerSys_notm}} zone can be upgraded with any issue.

### 08 January 2024
{: #powervs-vpc-jan08}
{: release-note}

Version 4.0.1 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
:   Version 4.0.1 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Upgrade TF IBM provider version to `1.61.0`
    - Change default {{site.data.keyword.powerSys_notm}} images for AIX and IBM i for all variations
    - Quickstart flavour now has a tshirt size `Custom (Configure in optional parameters)` in the dropdown. This is used when `custom_profile` needs to be used for custom deployments.

[Breaking change]{: tag-red}
: Version 4.0.1 includes backward-incompatible changes. Review the following information before you upgrade.
    - When upgrading to this version floating IPs are going to be deleted and recreated upon apply. This is due to a bug where the floating IPs were being created incorrectly in the Default resource group. Upon re-creation, the floating IPs will be created in the same resource group as the VSI.
    - Accordingly, please plan before upgrading incase this change will cause disruption for whatever is using the floating IPs.
    - 3 sleep resources will be deleted because of changes in the VPC landing zone module version

## December 2023
{: #powervs-vpc-2023-12}

### 05 December 2023
{: #powervs-vpc-dec05}
{: release-note}

Version 3.2.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
:   Version 3.2.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Support `MAD02` data center which is [PER enabled](/docs/power-iaas?topic=power-iaas-per).

## November 2023
{: #powervs-vpc-2023-11}

### 22 November 2023
{: #powervs-vpc-nov22}
{: release-note}

Version 3.1.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
:   Version 3.1.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Support `WDC06` data center which is [PER enabled](/docs/power-iaas?topic=power-iaas-per).


## October 2023
{: #powervs-vpc-2023-10}

### 27 October 2023
{: #powervs-vpc-oct27}
{: release-note}

Version 3.0.0 of the {{site.data.keyword.powerSysFull}} with VPC landing zone deployable architecture is available
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
        - The new landing zone version re-creates the 1 TB storage disk in a different resource group, so you will experience less down time.
        - When you upgrade, the deployable architecture will be down for about 20 minutes, and the Intel VSI will reboot.
   - If you deployed the QuickStart variation, you might want to create another deployable architecture rather than upgrade. The VM and VPC subnets are re-created, which might affect demos and PoCs.

## September 2023
{: #powervs-vpc-2023-09}

### 06 September 2023
{: #powervs-vpc-sep06}
{: release-note}

Version 2.0.0 available
:   Version 2.0.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Support RHEL 8.6 and SLES 15.4 images
    - Support `DAL10` data center which is [PER enabled](/docs/power-iaas?topic=power-iaas-per).

## August 2023
{: #powervs-vpc-2023-08}

### 23 August 2023
{: #powervs-vpc-aug23}
{: release-note}

Version 1.2.0 available
:   Version 1.2.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Introducing the new quickstart variant of {{site.data.keyword.powerSys_notm}} with VPC landing zone deployable architecture. For more information see [{{site.data.keyword.powerSys_notm}} with VPC landing zone quickstart variation](/docs/powervs-vpc?topic=powervs-vpc-automation-solution-overview#overview-powervs-workspace-import-variant)

## July 2023
{: #powervs-vpc-2023-07}

### 06 July 2023
{: #powervs-vpc-jul06}
{: release-note}

Version 1.1.0 available
:   Version 1.1.0 of the [{{site.data.keyword.powerSys_notm}} with VPC landing zone](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-inf-2dd486c7-b317-4aaa-907b-42671485ad96-global){: external} deployable architecture is available in the {{site.data.keyword.cloud_notm}} [catalog](/catalog#reference_architecture){: external}.
    - Introducing {{site.data.keyword.powerSys_notm}} with VPC landing zone
    - The {{site.data.keyword.powerSys_notm}} with VPC landing zone deployable architecture is released. You can use the deployable architecture to create an isolated {{site.data.keyword.powerSys_notm}} landscape connected with VPC landing zone.
