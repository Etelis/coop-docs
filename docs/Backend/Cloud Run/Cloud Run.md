---
title: Configuring Static IP Addresses in GCP
layout: page
---

## Overview

This guide provides instructions on how to configure a static external IP address for a VM instance in Google Cloud Platform (GCP). A static IP address ensures that the IP address does not change over time, unlike an ephemeral IP address, which can change every time the VM is restarted. This is particularly useful for services that rely on IP whitelisting or require a consistent IP address.

### Prerequisites

- Access to the Google Cloud Console.
- A VM instance created in your GCP project.
- The VM instance should be part of a VPC network.

### Assigning a Static IP Address

1. **Access the Google Cloud Console**

Navigate to the [Google Cloud Console](https://console.cloud.google.com/) and log in with your Google account.

2. **Navigate to VPC Network**

From the main navigation menu, go to **VPC network > IP addresses** to manage IP configurations for your project.

3. **Reserve a Static External IP Address**

- Click on **RESERVE EXTERNAL STATIC ADDRESS**.
- Provide a name for the IP address, for example, `co-op-world-server-22-ip`. Ensure the name adheres to GCP naming conventions, allowing lowercase letters, numbers, and hyphens.
- Select the **Region** that matches your VM instance's location, such as `europe-west1`.
- Leave the **IP version** as `IPv4`.
- Set the **Type** to `External`.
- Click **RESERVE** to allocate the static IP address.

### Configuring the VM Instance to Use the Static IP

1. **Assign the Static IP to Your VM Instance**

Navigate to the VM instances page by selecting **Compute Engine > VM instances** from the main navigation menu.

2. **Edit the VM Instance**

- Find the VM instance you wish to assign the static IP to, such as `co-op-world-server-22`.
- Click on the instance name to open its details page, then click **Edit**.
- Scroll down to the **Network interfaces** section and click on the pencil icon to edit the network interface.
- Under **External IP**, select the static IP address you reserved earlier from the dropdown list.
- Click **Done** to apply the changes, then scroll down to the bottom of the page and click **Save** to update the VM instance's configuration.

### Verification

Verify that the static IP address is correctly assigned to your VM instance:

- Navigate back to the **VPC network > IP addresses** section.
- Locate your newly reserved static IP address in the list. It should now show that it's in use by your specified VM instance.
