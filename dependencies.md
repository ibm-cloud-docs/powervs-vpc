---

copyright:
  years: 2023
lastupdated: "2023-07-10"

keywords:

subcollection: sap-powervs

---

{{site.data.keyword.attribute-definition-list}}

# Deployment dependencies
{: #powervs-automation-dependencies}

Power Virtual Server with VPC landing zone deployment by using deployable architectures is logically separated into the following steps:

1. Deploying VPC landing zone infrastructure. This landing zone acts as network security and management landscape for SAP solutions that are logically isolated to another infrastructure deployed as next. There might exist only one VPC landing zone per region in one IBM Cloud account.
2. Deploying Power Virtual Server with VPC landing zone. This deployed infrastructure hosts SAP solutions that are deployed as next. Provisioned IBM PowerVS workspace is connected to VPC landing zone. There might exist only one IBM PowerVS workspace per IBM PowerVS zone (data center) in one IBM Cloud account. Multiple PowerVS workspaces might be connected to the same VPC landing zone if the private CIDR network ranges of each IBM PowerVS infrastructure do not overlap. Multiple PowerVS workspaces in that case are connected to the same VPC landing zone and to each other. 

Each of these steps relies on the previous one. For instance, if you deploy Power Virtual Server with VPC landing zone deployment, you enter IBM Schematics workspace ID of another existing Power Virtual Server with VPC landing zone deployment. The prerequisite dependency is constrained by type. Means, for this deployable architecture not every VPC landing zone is accepted, but only the one created by Power Virtual Server with VPC landing zone deployable architecture.
{: note}

Certain steps are combined together and provided as one deployment step to simplify provisioning. For instances, this deployable architecture offers a full-stack variation that deploys both VPC landing zone and PowerVS workspace within one step. In addition you might deploy Power Virtual Server with VPC landing zone as an extension, which will create an additional PowerVS workspace and connect it with an existing VPC landing zone.
