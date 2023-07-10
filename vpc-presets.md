---

copyright:
  years: 2023
lastupdated: "2023-07-10"

keywords:

subcollection: powervs-vpc

---

{{site.data.keyword.attribute-definition-list}}

# VPC landing zone configurations
{: #powervs-automation-presets}

This solution is verified and supported with only the following configurations (presets) for a VPC landing zone. These presets must be selected or inserted when deploying the VPC landing zone either separately or as part of a new Power infrastructure with VPC landing zone deployment.
{: shortdesc}

- [RHEL secure landing zone preset](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure/blob/main/examples/ibm-catalog/presets/slz-for-powervs/rhel-vpc-pvs.preset.json){: external}. This preset creates a secure landing zone that is composed of three VPCs (edge, management, and workload) and of three VSIs with RHEL as operating system (bastion host, proxy server, management VSI)
- [SLES secure landing zone preset](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure/blob/main/examples/ibm-catalog/presets/slz-for-powervs/sles-vpc-pvs.preset.json){: external}. This preset creates a secure landing zone that is composed of three VPCs (edge, management, and workload) and of three VSIs with SLES as operating system (bastion host, proxy server, management VSI)

For more information regarding components that are defined in presets and the deployable architecture calling these presets, see [reference architecture for initial infrastructure deployment](/docs/deployable-reference-architectures?topic=deployable-reference-architectures-deploy-arch-ibm-pvs-inf-full-stack).

## Trusted zones specified by configurations
{: #powervs-automation-trusted-zones}

When you provision this landscape by using the VPC landing zone presets, the following trusted zones are configured. 

| Trusted zone name | Trusted zone type | Trusted zone purpose | Isolation methods |
| ----------------- | ----------------- | -------------------- | ----------------- |
| Edge VPC | VPC service | Isolate network connectivity to all resources located outside of the provisioned environment | Restrictions by network ACLs and VPC security groups |
| Management VPC | VPC service | Provide single entry point for landscape administrators | Restrictions by network ACLs and VPC security groups |
| Workload VPC | VPC service | Provide an isolated environment for services that are running on VPC instances | Restrictions by network ACLs and VPC security groups |
| SAP PowerVS | PowerVS workspace | Provide an isolated environment for SAP services that are running on PowerVS instances | Restrictions by VPC services connected with PowerVS workspace (Edge VPC, Management VPC, Workload VPC) |
{: caption="Table 1. Trusted zones" caption-side="bottom"}

## Data flows specified by configurations
{: #powervs-automation-data-flows}

When you provision this landscape by using the VPC landing zone presets, the following external data flows are configured. Additional data flows might be configured separately after deployment by managing VPC and PowerVS services directly.

| Source Zone | Destination Zone | Data Description | Protocol | Encryption | Authentication method | Direction |
| ----------- | ---------------- | ---------------- | -------- | ---------- | --------------------- | --------- |
| IBM Cloud Schematics IP addresses | Management VPC | SSH management connection | SSH (port 22) | SSH encryption chosen by customer | private/public SSH key | customer-sensitive | Outgoing |
| Edge VPC | Internet or other customer environment | OS and software patch management | HTTP/HTTPS (ports 80 and 443) | software dependent | software dependent | not customer-sensitive | Outgoing |
{: caption="Table 2. Data flow" caption-side="bottom"}

## Endpoints specified by configurations
{: #powervs-automation-endpoints}

When you provision this landscape by using the VPC landing zone presets, the following endpoints are configured. Additional endpoints might be configured separately after deployment by managing VPC and PowerVS services directly.

| Name              | Type | Description                     | Zone            | Exposed to zones                  | Authentication            |
| ----------------- | ---- | ------------------------------- | --------------- | --------------------------------- | ------------------------- |
| Management access | SSH  | SSH access for Linux root user. | Management VPC  | IBM Cloud Schematics IP addresses | Customer provided SSH key |
{: caption="Table 3. Endpoints configured for customer access" caption-side="bottom"}

Access to the landscape over the customer defined IP or from customer environment is not configured. Additional IP addresses for management VSI can be added to the network ACL of management VPC. As an alternative, a VPN connection can be set up. Currently, setting up access is considered as a manual post deployment task that you are responsible for.
{: note}
