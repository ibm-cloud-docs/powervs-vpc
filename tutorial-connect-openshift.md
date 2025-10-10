---

copyright:
  years: 2025
lastupdated: "2025-10-08"
keywords: vpn, openvpn, openshift
subcollection: powervs-vpc

---

{{site.data.keyword.attribute-definition-list}}

# Connect to your OpenShift cluster on {{site.data.keyword.powerSys_notm}}
{: #solution-connect-openshift-prerequisites}

This tutorial describes how to access the OpenShift cluster, via UI and CLI, deployed by the Quickstart OpenShift Variation of {{site.data.keyword.powerSysFull}} with VPC landing zone.
{: shortdesc}


## Prerequisites
{: #solution-connect-openshift-prerequisites}

- You have followed [Connect using a Client to Site VPN](/docs/powervs-vpc?topic=powervs-vpc-solution-connect-client-vpn) to setup connectivity.
- You have access to the terraform logs. You can find them either in your project's configuration or in the related Schematics workspace. These will be used to extract the initial cluster credentials to access the UI.


## Access the Cluster UI
{: #solution-connect-openshift-ui}

1. Locate the Cluster credentials in the terraform logs. Towards the end of the logs, locate the following section.

    ```log
    module.ocp_cluster_deployment.terraform_data.execute_playbooks[0] (remote-exec): time="2025-09-23T20:38:50Z" level=info msg="Install complete!"
    module.ocp_cluster_deployment.terraform_data.execute_playbooks[0] (remote-exec): time="2025-09-23T20:38:50Z" level=info msg="To access the cluster as the system:admin user when using 'oc', run\n    export KUBECONFIG=/root/ocp-powervs-deploy/auth/kubeconfig"
    module.ocp_cluster_deployment.terraform_data.execute_playbooks[0] (remote-exec): time="2025-09-23T20:38:50Z" level=info msg="Access the OpenShift web-console here: https://console-openshift-console.apps.<cluster_base_domain>"
    module.ocp_cluster_deployment.terraform_data.execute_playbooks[0] (remote-exec): time="2025-09-23T20:38:50Z" level=info msg="Login to the console with user: \"kubeadmin\", and password: \"<password>\""
    ```

1. Alternatively, you can [access the Cluster via oc CLI](#solution-connect-openshift-cli) and run the following command and extract the credentials from its output.

    ```bash
    openshift-install wait-for install-complete --dir=/root/ocp-powervs-deploy --log-level=debug
    ```

1. Enable the VPN connection
1. In your browser, navigate to `https://console-openshift-console.apps.<cluster_base_domain>` extracted above
1. Enter the cluster credentials extracted above and change your password if prompted
1. Congratulations! You can now manage your cluster from the UI


## Access the Cluster via oc CLI
{: #solution-connect-openshift-cli}

1. Enable the VPN connection
1. Use SSH to access the Network Services VSI

    ```bash
    ssh root@<network_services_ip> -i <path_to_private_key>
    ```

1. Optional. Depending on what you're trying to do, you may need to use Ansible Vault to decrypt the OCP config. Make sure to encrypt it again after you're done, it contains your API Key.

    ```bash
    ansible-vault decrypt /root/.powervs/config.json
    ansible-vault encrypt /root/.powervs/config.json
    ```

1. Export your KUBECONFIG

    ```bash
    export KUBECONFIG=/root/ocp-powervs-deploy/auth/kubeconfig
    ```

1. Run your `oc`commands, like for example:

    ```bash
    oc get all
    oc get nodes -o wide
    oc get secrets
    oc get pods
    ```


## Troubleshooting
{: #solution-connect-openshift-troubleshooting}

- Make sure you're VPN connection is enabled
- If you're unable to reach `https://console-openshift-console.apps.<cluster_base_domain>` from your local machine, check your DNS settings. Your local machine needs to use the DNS server that's part of the VPN profile to correctly resolve the cluster API. You can confirm by running `nslookup https://console-openshift-console.apps.<cluster_base_domain>` and checking that it's resolving to one of the load balancers.
