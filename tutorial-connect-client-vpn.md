---

copyright:
  years: 2023, 2024
lastupdated: "2024-09-16"
keywords:
subcollection: powervs-vpc
content-type: tutorial
services: vpc, secrets-manager, dl, schematics
account-plan: paid
completion-time: 1h

---

{{site.data.keyword.attribute-definition-list}}

# Connect using a client-to-site VPN
{: #solution-connect-client-vpn}
{: toc-content-type="tutorial"}
{: toc-services="vpc, secrets-manager, dl, schematics"}
{: toc-completion-time="1h"}

This tutorial dives into the fastest option to get up and running with a client VPN.
{: shortdesc}


## Download the OpenVPN client profile template
{: #solution-connect-client-vpn-openvpn-template}
{: step}

After the VPN server cloud resources are deployed, set up the OpenVPN client on devices that will access your landing zone.
By using the {{site.data.keyword.cloud_notm}} console:
1. Click the **Navigation menu** icon ![Navigation menu icon](../icons/icon_hamburger.svg "Menu"), and then click **VPC Infrastructure** > **VPNs** in the **Network** section to open the VPNs for VPC page.
1. Click the **Client-to-site servers** tab and select the client-to-site VPN server that you created.
1. Click the **Clients** tab. Then, click **Download client profile**.

## Download the OpenVPN client software
{: #solution-connect-client-vpn-openvpn-software}
{: step}

1.  Download and install the OpenVPN client application from https://openvpn.net/client/
1.  Open the OpenVPN client application, and import the `client2site-vpn.ovpn` file which was downloaded in Step 1.
1.  Enter one of the {{site.data.keyword.cloud_notm}} email addresses that was configured to access the VPN as the user ID.
1.  Go to [https://iam.cloud.ibm.com/identity/passcode](https://iam.cloud.ibm.com/identity/passcode) in your browser to generate a passcode. Copy the passcode.
1.  Return to the OpenVPN client application and paste the one-time passcode. 
1.  Click Continue.

## Test your VPN connection
{: #connect-client-vpn-connection}
{: step}

On the device that has the OpenVPN client, ping the `10.30.10.*` network (which is in your edge VPC).

```bash
ping 10.30.40.1
PING 10.30.40.1 (10.30.40.1): 56 data bytes
64 bytes from 10.30.40.1: icmp_seq=0 ttl=64 time=19.920 ms
64 bytes from 10.30.40.1: icmp_seq=1 ttl=64 time=19.301 ms
64 bytes from 10.30.40.1: icmp_seq=2 ttl=64 time=14.490 ms
64 bytes from 10.30.40.1: icmp_seq=3 ttl=64 time=20.896 ms
64 bytes from 10.30.40.1: icmp_seq=4 ttl=64 time=13.938 ms
^C
--- 10.30.40.1 ping statistics ---
5 packets transmitted, 5 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 13.938/17.709/20.896/2.904 ms
```

If you see no timeouts or other errors, your local workstation has connectivity to the VPC’s private network.

- To connect to the Ansible Node Intel instance:

    ```sh
    ssh root@<ansible_host_or_ip>
    ```

- To connect to the Network services running on network-services Intel instance:
    ```sh
    ssh root@<ntp_host_or_ip>
    ```

### Solving connectivity issues
{: #connect-client-vpn-connectivity}

In the following error, OpenVPN has an active connection, but can't reach a server on your private VPN subnet. Check the local network that your device connects through. Some newer routers allocate IP addresses in `10.*` range rather than `192.168.*`.

```text
error: dial tcp: lookup YOUR_SERVER_URL on 10.0.0.1:53:
read udp 10.0.0.2:0->10.0.0.1:53:
i/o timeout- verify you have provided the correct host and port and that the server is currently running.
```
{: screen}