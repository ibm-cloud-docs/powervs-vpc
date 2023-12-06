---

copyright:
  years: 2023
lastupdated: "2023-12-05"

keywords:

subcollection: powervs-vpc

---

{{site.data.keyword.attribute-definition-list}}

# Overview of {{site.data.keyword.powerSys_notm}} with VPC landing zone deployable architecture
{: #powervs-automation-overview}

Provisioning {{site.data.keyword.powerSys_notm}} with VPC landing zone by using deployable architectures provides an automated deployment method to create an isolated PowerVS workspace and connect it with IBM Cloud services and public internet. Network management components like DNS and NTP proxy servers and NFS server might be installed. Comparing the provisioning through the projects UI, user interaction is minimized and ready-to-go deployment time of a PowerVS workspace is reduced from days to less than 1 hour. 

Automated {{site.data.keyword.powerSys_notm}} with VPC landing zone provisioning that is described in this guide is based on {{site.data.keyword.cloud_notm}} catalog deployable architectures. In this documentation, we describe only specifics that are related to {{site.data.keyword.powerSys_notm}} with VPC landing zone deployable architecture.

In the following sections, the deployable architecture variants are described. 

## Create a new architecture - PowerVS workspace variation
{: #wrkspace-variant}

The {{site.data.keyword.powerSys_notm}} with VPC landing zone as variation 'Create a new architecture' deploys VPC services and a {{site.data.keyword.powerSys_notm}} workspace and interconnects them.

A proxy service for public internet access from the PowerVS workspace is configured. You can optionally configure some management components on VPC (such as an NFS server, NTP forwarder, and DNS forwarder).

For more information on how to deploy, see [Deploying the {{site.data.keyword.powerSys_notm}} with VPC landing zone - 'PowerVS workspace' Variation](https://cloud.ibm.com/docs/powervs-vpc?topic=powervs-vpc-powervs-automation-deploy).

## Extend {{site.data.keyword.powerSys_notm}} with VPC landing zone - PowerVS Workspace variation
{: #extnsn-variant}

This PowerVS Workspace variation has a prerequisite. You must deploy the 'Create a new architecture PowerVS workspace' variant.
{: important}

The {{site.data.keyword.powerSys_notm}} with VPC landing zone as variation 'Extend {{site.data.keyword.powerSys_notm}} with VPC landing zone' creates an additional {{site.data.keyword.powerSys_notm}} workspace and connects it with already created {{site.data.keyword.powerSys_notm}} with VPC landing zone. It builds on existing {{site.data.keyword.powerSys_notm}} with VPC landing zone deployed as a variation 'Create a new architecture'.
This is typically used for High Availability scenarios in same regions.

## Create a new architecture - PowerVS Quickstart variation
{: #qkstart-variant}

You can now deploy a {{site.data.keyword.powerSys_notm}} (PowerVS) with VPC landing zone which creates VPC services, a {{site.data.keyword.powerSys_notm}} workspace and interconnect them. 

You can run AIX, IBM i, and Linux images on your virtual server instances. Select the required T-shirt size and a virtual server instance with chosen T-shirt size or custom configuration is deployed. The T-shirt sizes and the configuration parameters mapping is shown in the table below:

|  | XS | S | M | L |
|---------------------- | ------------------------- | ------------------------- | -------------------------  | ------------------------- |
| Cores | 1 | 4 | 8 | 15 |
| Memory | 32 | 128 | 256 | 512 |
| Storage Tier-1 (GB) | 100 | 500 | 1000 | 2000 |
{: class="simple-tab-table"}
{: tab-group="t-shirt size"}
{: caption="Table 1. T-shirt size and configuration mapping" caption-side="top"}
{: #resize_core_memory-1}
{: tab-title="AIX"}

|  | XS | S | M | L |
|---------------------- | ------------------------- | ------------------------- | -------------------------  | ------------------------- |
| Cores | 0.25 | 1 | 2 | 4 |
| Memory | 8 | 32 | 64 | 132 |
| Storage Tier-1 (GB) | 100 | 500 | 1000 | 2000 |
{: class="simple-tab-table"}
{: tab-group="t-shirt size"}
{: caption="Table 1. T-shirt size and configuration mapping" caption-side="top"}
{: #resize_core_memory-1}
{: tab-title="IBM i"}

|  | US1 \n Test/Dev |
|---------------------- | ------------------------- |
| Cores | 4 |
| Memory | 128 |
| Storage Tier-1 (GB) | 750 |
{: class="simple-tab-table"}
{: tab-group="t-shirt size"}
{: caption="Table 1. T-shirt size and configuration mapping" caption-side="top"}
{: #resize_core_memory-1}
{: tab-title="SAP HANA (Red Hat)"}


A proxy service for public internet access from the PowerVS workspace is also configured. You can optionally configure some management components on VPC such as an NFS server, NTP forwarder, and DNS forwarder.

For more information on how to deploy, see [Deploying the {{site.data.keyword.powerSys_notm}} with VPC landing zone - 'PowerVS quickstart' variation](https://cloud.ibm.com/docs/powervs-vpc?topic=powervs-vpc-powervs-quickstart-deploy).

## Other PowerVS related deployable architectures
{: #powervs-automation-solution-components}

In addition to the {{site.data.keyword.powerSys_notm}} with VPC landing zone other deployable architectures and terraform based solutions might be deployed. 

- [{{site.data.keyword.powerSys_notm}} for SAP HANA deployable architecture](/docs/sap-powervs)
- [FalconStor StorSafe VTL for PowerVS Cloud](https://falconstor-download.s3.us-east.cloud-object-storage.appdomain.cloud/FalconStor%20VTL%20for%20IBM%20Deployment%20Guide.pdf){: external}

