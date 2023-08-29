---

copyright:
  years: 2023
lastupdated: "2023-08-24"

keywords:

subcollection: powervs-vpc

---

{{site.data.keyword.attribute-definition-list}}

# Overview of Power Virtual Server with VPC landing zone deployable architecture
{: #powervs-automation-overview}

Provisioning Power Virtual Server with VPC landing zone by using deployable architectures provides an automated deployment method to create an isolated PowerVS workspace and connect it with IBM Cloud services and public internet. Network management components like DNS and NTP proxy servers and NFS server might be installed. Comparing the provisioning through the projects UI, user interaction is minimized and ready-to-go deployment time of a PowerVS workspace is reduced from days to less than 1 hour. 

Automated Power Virtual Server with VPC landing zone provisioning that is described in this guide is based on {{site.data.keyword.cloud_notm}} catalog deployable architectures. In this documentation, we describe only specifics that are related to Power Virtual Server with VPC landing zone deployable architecture.

In the following sections, the deployable architecture variants are described. 

## Quickstart variation
{: #qkstart-variant}

You can now deploy a Power Virtual Server (PowerVS) with VPC landing zone to creates VPC services, a Power Virtual Server workspace and interconnect them. 

You can run AIX, IBM i, and Linux images on your virtual server instances. Select the required T-shirt size and a virtual server instance with chosen T-shirt size or custom configuration is deployed. The T-shirt sizes and the configuration parameters mapping is shown in the table below:

|  | XS | S | M | L |
|---------------------- | ------------------------- | ------------------------- | -------------------------  | ------------------------- |
| Cores | 1 | 4 | 8 | 15 |
| Memory | 32 | 128 | 256 | 512 |
| Stprage Tier-1 (GB) | 100 | 500 | 1000 | 2000 |
{: class="simple-tab-table"}
{: tab-group="t-shirt size"}
{: caption="Table 1. T-shirt size and configuration mapping" caption-side="top"}
{: #resize_core_memory-1}
{: tab-title="AIX"}

|  | XS | S | M | L |
|---------------------- | ------------------------- | ------------------------- | -------------------------  | ------------------------- |
| Cores | 0.25 | 1 | 2 | 4 |
| Memory | 8 | 32 | 64 | 132 |
| Stprage Tier-1 (GB) | 100 | 500 | 1000 | 2000 |
{: class="simple-tab-table"}
{: tab-group="t-shirt size"}
{: caption="Table 1. T-shirt size and configuration mapping" caption-side="top"}
{: #resize_core_memory-1}
{: tab-title="IBM i"}

|  | US1 \n Test/Dev | Bh1 \n OLAP | UMH \n OLTP |
|---------------------- | ------------------------- | ------------------------- | -------------------------  |
| Cores | 4 | 16 | 16 |
| Memory | 128 | 1600 | 768 |
| Stprage Tier-1 (GB) | 500 | 3170 | 2490 |
{: class="simple-tab-table"}
{: tab-group="t-shirt size"}
{: caption="Table 1. T-shirt size and configuration mapping" caption-side="top"}
{: #resize_core_memory-1}
{: tab-title="SAP HANA (Red Hat)"}


A proxy service for public internet access from the PowerVS workspace is also configured. You can optionally configure some management components on VPC such as an NFS server, NTP forwarder, and DNS forwarder.

For more information on how to deploy, see [Deploying the Power Virtual Server with VPC landing zone - 'PowerVS quickstart' variation](https://test.cloud.ibm.com/docs/powervs-vpc?topic=powervs-vpc-powervs-quickstart-deploy).

## PowerVS workspace variation
{: #wrkspace-variant}

New deployment of the Power Virtual Server with VPC landing zone creates VPC services and a Power Virtual Server workspace and interconnects them.

A proxy service for public internet access from the PowerVS workspace is configured. You can optionally configure some management components on VPC (such as an NFS server, NTP forwarder, and DNS forwarder).

For more information on how to deploy, see [Deploying the Power Virtual Server with VPC landing zone - 'PowerVS workspace' Variation](https://test.cloud.ibm.com/docs/powervs-vpc?topic=powervs-vpc-powervs-automation-deploy).

## Extension variation
{: #extnsn-variant}

This extension variation has a prerequisite. You must deploy either the PowerVS workspace variant or the PowerVS quickstart variant.
{: important}

The Power Virtual Server with VPC landing zone as variation 'Extend Power Virtual Server with VPC landing zone' creates an additional Power Virtual Server workspace and connects it with already created Power Virtual Server with VPC landing zone. It builds on existing Power Virtual Server with VPC landing zone deployed as a variation 'Create a new architecture'.

## Other PowerVS related deployable architectures
{: #powervs-automation-solution-components}

In addition to the Power Virtual Server with VPC landing zone other deployable architectures and terraform based solutions might be deployed. 

- [Power Virtual Server for SAP HANA deployable architecture](/docs/sap-powervs)
- [FalconStor StorSafe VTL for PowerVS Cloud](https://falconstor-download.s3.us-east.cloud-object-storage.appdomain.cloud/FalconStor%20VTL%20for%20IBM%20Deployment%20Guide.pdf){: external}

