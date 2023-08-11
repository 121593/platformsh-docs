---
title: Optional features
weight: 4
description: Optional features are available on your {{% names/dedicated-gen-3 %}} project.
---

{{% description %}}

## Multiple availability zones

The default configuration for Dedicated clusters is to launch them into a single availability zone (AZ)
for the following reasons:

- The members of your cluster communicate with each other via TCP to perform DB replication,
  cache lookup, and other associated tasks.
  Therefore, the latency between data centers or AZs can become a significant performance liability.
  When your entire cluster is deployed within a single AZ, the latency between cluster members is minimal.
  This has a direct effect on perceived end-user performance.

- Network traffic between AZs is billed, whereas intra-AZ traffic isn't.
  So launching Dedicated clusters across multiple AZs leads to higher costs for decreased performance.

If you prefer the peace of mind of hosting across multiple AZs,
you can request a different configuration.
But note that multiple-AZ configurations don't improve the contractual 99.99% uptime SLA
(nor does the standard, single-AZ configuration decrease the 99.99% uptime SLA).
Platform.sh is responsible for meeting the 99.99% uptime SLA no matter what,
so multiple-AZ deployments should only be considered in cases where they're truly appropriate.

Multi-AZ deployments are available only on select AWS regions.

## SFTP accounts

In addition to SSH accounts, SFTP accounts can be created with a custom user/password that are restricted to certain directories. 
These directories must be one of the writeable [mounts](../../create-apps/app-reference.md#mounts)
(or rather, there’s no point assigning them to the read-only code directory).

There is no cost for this configuration, and it can be requested at any time via a [support ticket](https://console.platform.sh/-/users/~/tickets). 
SSH public key based authentication is also supported on the SFTP account.