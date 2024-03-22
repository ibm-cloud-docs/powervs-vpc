---

copyright:
  years: 2023
lastupdated: "2023-04-26"

subcollection: powervs-vpc

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Understanding your responsibilities when you use Power Virtual Server with VPC landing zone deployable architecture
{: #responsibilities}

Learn about the management responsibilities and terms and conditions that you have when you use the Power Virtual Server with VPC landing zone deployable architecture.
{: shortdesc}

- For more information about the responsibilities for you and for {{site.data.keyword.IBM}} when you use a deployable architecture, see [Understanding your responsibilities when you use deployable architectures](/docs/secure-enterprise?topic=secure-enterprise-responsibilities-deployable-architectures).
- For a high-level view of the service types in {{site.data.keyword.cloud}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for using {{site.data.keyword.cloud_notm}} products](/docs/overview?topic=overview-shared-responsibilities).
- For the overall terms of use, see [{{site.data.keyword.cloud}} Terms and Notices](/docs/overview?topic=overview-terms).

Review the following section for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use the Power Virtual Server with VPC landing zone deployable architecture.

## Security and regulation compliance
{: #sap-powervs-automation-security}

Security and regulation compliance includes tasks such as security controls implementation and compliance certification.

| Task             | IBM responsibility | Your responsibility |
|------------------|--------------------------|------------------------|
| Ensure that the operating system image does not contain any vulnerabilities. | IBM Cloud provided and verified RHEL and SLES operating system images are used. After deployment, operating system images are updated to the newest state in the defined minor release. Official RHEL and SLES software repositories are used for installation of additional software components (like SQUID proxy). | Customer is responsible to keep the operating system secure and compliant after deployment. |
{: caption="Table 1. Security and compliance responsibilities for provisioned components}
