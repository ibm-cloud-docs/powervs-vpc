---

copyright:
  years: 2023, 2024
lastupdated: "2024-10-31"
keywords: powervs, landing zone, sap, automation, deployable architecture
subcollection: powervs-vpc

---

{{site.data.keyword.attribute-definition-list}}

# Overview of {{site.data.keyword.powerSys_notm}} with VPC landing zone deployable architectures
{: #automation-solution-overview}

Provisioning {{site.data.keyword.powerSys_notm}} with VPC landing zone by using deployable architectures provides an automated deployment method to create an isolated {{site.data.keyword.powerSys_notm}} workspace and connect it with IBM Cloud services and public internet. Network management components like DNS, NTP, proxy servers and NFS as a Service might be installed. Comparing the provisioning through the projects UI, user interaction is minimized and ready-to-go deployment time of a {{site.data.keyword.powerSys_notm}} workspace is reduced from days to less than 1 hour. 

Automated {{site.data.keyword.powerSys_notm}} with VPC landing zone provisioning that is described in this guide is based on {{site.data.keyword.cloud_notm}} catalog deployable architectures. In this documentation, we describe only specifics that are related to {{site.data.keyword.powerSys_notm}} with VPC landing zone deployable architecture.

In the following sections, the deployable architecture variants are described. 

![Solution Overview](images/overview-solutions.png){: caption="Solution Overview" caption-side="center"}

## Standard variation
{: #overview-standard-variant}

This deployable architecture variation supports these features:
- A **VPC Infrastructure** with the following components:
    - One RHEL VSI for one management (jump/bastion) VSI
    - One RHEL VSI for network-services configured as squid proxy, NTP and DNS servers(using Ansible Galaxy collection roles [ibm.power_linux_sap collection](https://galaxy.ansible.com/ui/repo/published/ibm/power_linux_sap/). This VSI also acts as central ansible execution node
    - Optional [Client to site VPN server](https://cloud.ibm.com/docs/vpc?topic=vpc-vpn-client-to-site-overview)
    - Optional [File storage share](https://cloud.ibm.com/docs/vpc?topic=vpc-file-storage-create&interface=ui)
    - Optional [Application load balancer](https://cloud.ibm.com/docs/vpc?topic=vpc-load-balancers&interface=ui)
    - IBM Cloud Object storage(COS) Virtual Private endpoint gateway(VPE)
    - IBM Cloud Object storage(COS) Instance and buckets
    - VPC flow logs
    - KMS keys
    - Activity tracker
    - Optional Secrets Manager Instance Instance with private certificate
- A local or global **transit gateway**
- A **{{site.data.keyword.powerSys_notm}}** workspace with the following network topology:
    - Creates two private networks: a management network and a backup network
    - Attaches the {{site.data.keyword.powerSys_notm}} workspace to transit gateway
    - Creates an SSH key
    - Imports catalog stock images

## Extend {{site.data.keyword.powerSys_notm}} with VPC landing zone - Standard variation
{: #overview-standard-extend-variant}

This variation has a prerequisite. You must deploy the 'Create a new architecture Standard' variant first.
{: important}

The 'Extend {{site.data.keyword.powerSys_notm}} with VPC landing zone' variation creates an additional {{site.data.keyword.powerSys_notm}} workspace and connects it to the existing {{site.data.keyword.powerSys_notm}} with VPC landing zone. It builds on existing {{site.data.keyword.powerSys_notm}} with VPC landing zone deployed as a variation 'Create a new architecture'.
This is typically used for High Availability scenarios in the same regions.

This deployable architecture variation supports these features:
- A **{{site.data.keyword.powerSys_notm}} workspace** with the following network topology:
    - Creates two private networks: a management network and a backup network
    - Attaches the {{site.data.keyword.powerSys_notm}} workspace to transit gateway
    - Creates an SSH key
    - Imports catalog stock images


## Quickstart variation
{: #overview-quickstart-variant}

This deployable architecture variation supports these features:
- A **VPC Infrastructure** with the following components:
    - One RHEL VSI for one management (jump/bastion) VSI
    - One RHEL VSI for network-services configured as squid proxy, NTP and DNS servers(using Ansible Galaxy collection roles [ibm.power_linux_sap collection](https://galaxy.ansible.com/ui/repo/published/ibm/power_linux_sap/). This VSI also acts as central ansible execution node.
    - Optional [Client to site VPN server](https://cloud.ibm.com/docs/vpc?topic=vpc-vpn-client-to-site-overview)
    - Optional [File storage share](https://cloud.ibm.com/docs/vpc?topic=vpc-file-storage-create&interface=ui)
    - Optional [Application load balancer](https://cloud.ibm.com/docs/vpc?topic=vpc-load-balancers&interface=ui)
    - IBM Cloud Object storage(COS) Virtual Private endpoint gateway(VPE)
    - IBM Cloud Object storage(COS) Instance and buckets
    - VPC flow logs
    - KMS keys
    - Activity tracker
    - Optional Secrets Manager Instance Instance with private certificate.
- A local or global **transit gateway**
- A **{{site.data.keyword.powerSys_notm}} workspace** with the following network topology:
    - Creates two private networks: a management network and a backup network
    - Attaches the {{site.data.keyword.powerSys_notm}} workspace to transit gateway
    - Creates an SSH key
    - Imports cloud catalog stock images
- A **{{site.data.keyword.powerSys_notm}} Instance** with following options:
    - t-shirt profile (Aix/IBMi/SAP Image)
    - Custom profile ( cores, memory, storage and image)
    - 1 volume

You can run AIX, IBM i, and Linux images on your virtual server instances. Select the required T-shirt size and a virtual server instance with chosen T-shirt size or custom configuration is deployed. The T-shirt sizes and the configuration parameters mapping are shown in the following table:

|  | XS | S | M | L |
|---------------------- | ------------------------- | ------------------------- | -------------------------  | ------------------------- |
| Cores | 1 | 4 | 8 | 15 |
| Memory | 32 | 128 | 256 | 512 |
| Storage Tier-3 (GB) | 100 | 500 | 1000 | 2000 |
{: class="simple-tab-table"}
{: tab-group="t-shirt size"}
{: caption="T-shirt size and configuration mapping" caption-side="top"}
{: #resize_core_memory-1}
{: tab-title="AIX"}

|  | XS | S | M | L |
|---------------------- | ------------------------- | ------------------------- | -------------------------  | ------------------------- |
| Cores | 0.25 | 1 | 2 | 4 |
| Memory | 8 | 32 | 64 | 132 |
| Storage Tier-3 (GB) | 100 | 500 | 1000 | 2000 |
{: class="simple-tab-table"}
{: tab-group="t-shirt size"}
{: caption="T-shirt size and configuration mapping" caption-side="top"}
{: #resize_core_memory-2}
{: tab-title="IBM i"}

|  | US1 \n Test/Dev |
|---------------------- | ------------------------- |
| Cores | 4 |
| Memory | 128 |
| Storage Tier-3 (GB) | 750 |
{: class="simple-tab-table"}
{: tab-group="t-shirt size"}
{: caption="T-shirt size and configuration mapping" caption-side="top"}
{: #resize_core_memory-3}
{: tab-title="SAP HANA (RHEL/SLES)"}

## Import variation
{: #overview-powervs-workspace-import-variant}

Create an IBM Cloud schematics workspace for your pre-existing VPC and {{site.data.keyword.powerSys_notm}} infrastructure resources using the new {{site.data.keyword.powerSys_notm}} (PowerVS) with VPC landing zone variation - 'Import {{site.data.keyword.powerSys_notm}} Workspace'. 

This variation helps to install the deployable architecture ['Power Virtual Server for SAP HANA'](https://cloud.ibm.com/catalog/architecture/deploy-arch-ibm-pvs-sap-9aa6135e-75d5-467e-9f4a-ac2a21c069b8-global) on top of a pre-existing {{site.data.keyword.powerSys_notm}}(PowerVS) landscape. 'Power Virtual Server for SAP HANA' automation requires a schematics workspace id for installation. The 'Import' solution creates a schematics workspace by taking pre-existing VPC and {{site.data.keyword.powerSys_notm}} infrastructure resource details as inputs. The ID of this schematics workspace will be the pre-requisite workspace id required by 'Power Virtual Server for SAP HANA' to create and configure the {{site.data.keyword.powerSys_notm}} instances for SAP on top of the existing infrastructure. 

Check the pre-requisites for this variation [here](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure/tree/main/solutions/import#pre-requisites).


## Other {{site.data.keyword.powerSys_notm}} related deployable architectures
{: #overview-automation-solution-components}

In addition to the {{site.data.keyword.powerSys_notm}} with VPC landing zone other deployable architectures and terraform based solutions might be deployed. 

- [{{site.data.keyword.powerSys_notm}} for SAP HANA deployable architecture](/docs/sap-powervs)
- [FalconStor StorSafe VTL for {{site.data.keyword.powerSys_notm}} Cloud](https://falconstor-download.s3.us-east.cloud-object-storage.appdomain.cloud/FalconStor%20VTL%20for%20IBM%20Deployment%20Guide.pdf){: external}
