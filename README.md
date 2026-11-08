# Cloud File Server: Managed, Hybrid, or Self-Hosted? Three Routes Compared, Plus the Three-Meter Billing Structure Most Quotes Leave Out (Full Plan Table)

A cloud file server is a file server people reach over the internet: browser, mapped drive, desktop client or phone app, with sharing done by link instead of email attachment. Three routes get you there, and they fail in different ways — a fully managed cloud file system, a hybrid gateway bolted onto the Windows server you already run, or a file server you build yourself on rented hardware.

The billing model decides more than the feature list does. Managed file systems meter three things separately: storage capacity per GB-month, throughput per MBps-month, and SSD IOPS above the **3 IOPS per GB** that comes bundled with every gigabyte of SSD storage. Backup storage is billed per GB-month on top. There's no minimum commitment, but there's also no single number to anchor on, which is why two teams holding the same 2 TB of files can end up on very different invoices.

> **Quick version.** Data allowed to leave your building and no appetite for patching → managed file system. Data has to stay put and staff expect drive letters → hybrid gateway in front of your existing server. Want a flat monthly bill, root access and full control, and will own the OS, the backups and the ransomware hardening → rent the hardware and run the file service yourself. SpinServers lists a Xeon E3-1280 v5 with 32 GB RAM and 1 TB NVMe from **$79.00/mo**, and a 32 vCPU / 32 GB / 500 GB SSD KVM instance from **$89.00/mo**.
> 👉 [Check the live server listings and current stock](https://bit.ly/Spinservers)

## What a cloud file server has to do before you compare vendors

Strip the marketing and the job is narrow: centralized storage plus a workspace, where files can be opened, edited, shared or deleted from any internet-connected device, and where sharing happens through a web URL rather than an attachment. Access arrives through browsers, mobile apps and standard PC/Mac clients, traffic runs over HTTPS, and remote access replaces the VPN-and-RDP routine.

Deployment model decides which vendors you're even allowed to talk to:

- **Public.** A third-party provider serves you from multi-tenant infrastructure spread across its own data centres, typically pay-per-use with charges tied to the frequency and volume of data accessed.
- **Private.** The file service runs in your data centre or in a dedicated hosted environment, single-tenant, for organisations with strict customization, control or regulatory requirements.
- **Hybrid.** Files move between public and private infrastructure, or stay local while a cloud layer handles access and sharing.

Four things are worth verifying in writing before you sign: API integration with the applications you already run, the physical location of the data (latency plus disaster exposure), the security stack (firewall, endpoint monitoring, access control, DLP, ransomware protection and recovery), and performance under real conditions including how planned and unplanned downtime is handled. Access control usually rides on a cloud identity service with MFA and SSO, and least-privilege permissions are the foundation of any zero-trust model you plan to build later.

## The route you can price today: SpinServers VPS and dedicated servers

SpinServers sells infrastructure, not a managed SMB service. You rent a KVM VPS or a dedicated machine, pick the OS at install, and run the file server software yourself. That makes it the third route in this article: maximum control, flat billing, and every operational duty stays with you.

| Plan | Core specs | Transfer / port | Listed price (USD/mo) | Order |
| --- | --- | --- | --- | --- |
| Simple Application Server | Intel 2 vCPU · 2 GB DDR4 · 40 GB RAID-10 SSD | 4 TB · 1 Gbps | Not listed on the page | [Start with the entry VPS](https://bit.ly/Spinservers) |
| Simple Application Server | 6 vCPU · 8 GB DDR4 · 120 GB RAID-10 SSD | 8 TB · 1 Gbps | Not listed on the page | [Order the 6 vCPU VPS](https://bit.ly/Spinservers) |
| Simple Application Server | 8 vCPU · 8 GB DDR4 · 160 GB RAID-10 SSD | 10 TB · 1 Gbps | Not listed on the page | [Order the 8 vCPU VPS](https://bit.ly/Spinservers) |
| Simple Application Server | 12 vCPU · 12 GB DDR4 · 160 GB RAID-10 SSD | 10 TB · 1 Gbps | from $62.00 | [Order the 12 vCPU VPS](https://bit.ly/Spinservers) |
| Hybrid KVM | 32 vCPU · 32 GB RAM · 500 GB SSD | 20 TB · 1 Gbps | from $89.00 | [Order the 32 vCPU Hybrid KVM](https://bit.ly/Spinservers) |
| Xeon E3-1280 v5 (Dallas / San Jose) | 4 vCPU · 32 GB RAM · 1 TB NVMe | 30 TB | from $79.00 | [Order the E3-1280 v5](https://bit.ly/Spinservers) |
| Dual Xeon Gold 6148 (Dallas) | 40 vCPU · 256 GB RAM · 3.84 TB SSD | 30 TB | from $235.00 | [Order the dual Gold 6148](https://bit.ly/Spinservers) |
| Dual Xeon Platinum 8173M (Dallas) | 56 vCPU · 512 GB RAM · 7.68 TB SSD | 30 TB | from $390.00 | [Order the dual Platinum 8173M](https://bit.ly/Spinservers) |

Every instance ships with one IPv4 and one IPv6 address and a 1 Gbps port. The smaller VPS tiers don't carry a "starting from" figure on the page, so confirm the configured price against the live store before you commit. Stock and promotional configurations change; the table reflects what the store listed when this was written.

Two configurations deserve a comment. The **$79 dedicated E3-1280 v5** is the interesting one for a file server: 1 TB of NVMe and 32 GB of RAM at a fixed monthly price, with 30 TB of transfer, which is far more than a 40-person office will push through SMB sync. The **32 vCPU Hybrid KVM at $89** is the wrong shape for file serving — vCPU count buys you nothing when the bottleneck is disk and network — but it's a reasonable pick if the same box also has to run a database or a build server.

## Route 1: fully managed file systems

Amazon FSx offers four file systems — NetApp ONTAP, OpenZFS, Windows File Server and Lustre — and the choice usually comes down to what your team already knows or which feature set matches the workload. FSx for Windows File Server is the one that maps onto a classic office file share: it's built on Windows Server, speaks SMB, and can be mounted from up to thousands of compute instances. Clients can run any Windows version from Windows Server 2008 and Windows 7 onward, plus current Linux and macOS. On-premises access goes through AWS Direct Connect or AWS VPN, cross-VPC and cross-account access through VPC Peering or Transit Gateway, and FSx File Gateway adds a local cache for people who need low-latency access from the office.

Storage can be SSD or HDD, throughput is provisioned independently of capacity, and you choose Single-AZ or Multi-AZ. Multi-AZ runs an active/standby pair with synchronous replication and automatic failover; Single-AZ still replicates within the zone. Data at rest is encrypted with AWS KMS, deduplication and compression are built in, and usage quotas are supported at user and folder level through File Server Resource Manager.

Azure Files covers the same ground with SMB and NFS shares spanning Azure, on-premises, containers and virtual desktops. Azure File Sync modernizes an existing Windows file server while keeping the access patterns staff are used to, and Azure Arc extends Windows Server environments into the same management plane. Capacity, IOPS and throughput are provisioned independently on both HDD and SSD shares, with credit-based bursting for spikes. Authentication is identity-based through Azure RBAC rather than storage account keys, and share, directory and file permissions use standard Windows ACLs.

## What managed file storage actually bills you for

Take the three meters one at a time, because each one is a place where a quote can be under-specified:

1. **Storage capacity**, priced per GB-month.
2. **SSD IOPS above the default 3 IOPS per GB** included with SSD storage, priced per IOPS-month. A 500 GB SSD volume therefore ships with 1,500 IOPS. If your workload needs 10,000, you buy the difference as its own line item.
3. **Throughput capacity**, priced per MBps-month, provisioned separately from capacity.
4. **Backup storage**, priced per GB-month, billed on top of all three.

That 3 IOPS/GB baseline is the single most useful number to carry into a sizing conversation. Small volumes get small IOPS allowances by default, and file servers with lots of simultaneous users hit IOPS ceilings long before they run out of space. Provisioning 5 TB when you only need 500 GB doesn't just cost more in storage; it changes the IOPS maths as well.

Deduplication and compression are the offsetting lever, and the savings depend entirely on what you store. Typical ranges: **50–60%** for general-purpose file shares, **30–50%** for user documents, and **70–80%** for software development datasets. Turn it on for anything with repeated content; a media archive of already-compressed video won't benefit much.

👉 [Compare the dedicated and VPS configurations that replace those meters with one flat bill](https://bit.ly/Spinservers)

## Peak IOPS and persistent IOPS are not the same number

Vendor pages quote the biggest figure in the deck. On FSx for Windows File Server, cached access to frequently used data reaches up to **21 GB/s of throughput and millions of IOPS**; access that misses the cache and hits persistent disk tops out at **12 GB/s and 350,000 IOPS**. Both numbers are real; they describe different access patterns. A workload that streams large files sequentially and a workload that opens 40,000 small documents a day will land on opposite sides of that gap.

SMB Multichannel matters for a different reason: it lets a single client use multiple network connections, so one workstation can actually consume the throughput and IOPS you provisioned. Without it, the per-client ceiling becomes the limit no matter what the file system can deliver.

## Permissions, identity and where the audit trail lands

FSx for Windows File Server integrates with your on-premises Microsoft Active Directory or with AWS Managed AD, and permissions are standard Windows ACLs. Network-level control comes from VPC security groups, API actions are governed by IAM, administrative actions are logged in CloudTrail, and storage and performance metrics flow to CloudWatch. End-user access can be audited through Windows event logs forwarded to CloudWatch Logs or Kinesis Data Firehose, which can archive to S3, trigger Lambda, or feed Splunk and Datadog. File screening blocks file types you don't want on the share, and those events land in the same logging pipeline.

If your files fall under PCI DSS, ISO 9001/27001/27017/27018, SOC 1/2/3, HIPAA or FedRAMP, FSx has been assessed against all of them. Encryption in transit is automatic when clients support SMB 3.0 or newer, which covers Windows Server 2012 and Windows 8 onward and Linux clients with Samba 4.2 or later. Older clients connect, but they don't get that automatic transport encryption, which is worth checking before you migrate a lab full of legacy machines.

## Route 2: keep the file server, put a cloud front door on it

CentreStack takes the opposite approach: it adds cloud file services — remote access, secure external sharing, data protection — to the file server you already own, while keeping your existing security safeguards, permission controls and data ownership. Two deployment shapes:

- **Hybrid file servers.** A Cloud Server Agent migrates file shares and keeps them in bidirectional sync. Legacy apps and users keep hitting the share directly while folders, permissions and users replicate to online storage. You can run in hybrid mode indefinitely and retire the old file server when you're ready.
- **File server as the cloud.** The file server stays on-premises or in your own data centre, CentreStack sits on the same network, and **no data is replicated to third-party locations**. Remote access runs over HTTPS, and existing NTFS and Active Directory security applies unchanged.

Practical features include a cloud-mapped drive letter without a VPN, fine-grained folder permissions that mirror NTFS, on-demand sync that caches only the files a user needs, encryption of remote agent caches with the ability to revoke access from a central console, and full file locking from the cloud. The vendor's argument for this design is that exposing SMB shares over a VPN can expose security weaknesses to malware, and that SMB drive mapping over a VPN is slow because it was built for local mapping. That's a vendor position, not an independent benchmark, but the underlying point about SMB over VPN being awkward at scale is worth weighing if remote access is your main pain.

## Backups and ransomware recovery

On FSx for Windows File Server, backups are automatic: daily, file-system-consistent, highly durable copies to S3 taken through the Volume Shadow Copy Service, with the option to take extra backups on demand. AWS Backup adds policy-driven schedules, cross-Region replication is available, and end users can restore their own files without opening a ticket. That last feature removes a surprising amount of helpdesk load.

Self-hosted changes the picture entirely. You get root, so you also get to design snapshot schedules, keep an off-box or offline copy that ransomware can't encrypt, and actually test a restore. A file server without a tested restore path is a liability with a NIC.

## Route 3: build the cloud file server on your own hardware

Rent a dedicated machine, install Windows Server file services, Samba on Linux, or a web-based sync layer, and you have a cloud file server with a fixed monthly cost and no per-GB, per-IOPS or per-MBps meters. What you don't get is a managed control plane, so patching, monitoring, TLS certificates, backup verification and access review are yours.

Three checks before ordering:

1. **OS licensing.** Confirm what your chosen Windows or Linux image includes and what it costs at checkout. A Windows Server licence is a real line item and it isn't part of the hardware price.
2. **Storage growth path.** The E3-1280 v5 comes with 1 TB of NVMe; the dual Gold 6148 with 3.84 TB. Make sure the chassis can take more disks before your share outgrows the box.
3. **Transfer allowance against sync volume.** A 30 TB monthly allowance covers a lot of SMB traffic, but if you plan to replicate the whole share to a second site nightly, do that arithmetic first.

👉 [See which dedicated configurations are available right now](https://bit.ly/Spinservers)

## Which route fits your situation

- **Data legally or contractually cannot leave your premises** → file server as the cloud, with CentreStack or an equivalent layer providing HTTPS access. No replication to a third party.
- **Windows ACLs, drive letters and AD group policy are non-negotiable, and staff resist change** → hybrid file servers, or FSx for Windows File Server if you're ready to hand over the patching.
- **You want the least operational work and can accept three-meter billing** → a managed file system. Budget for IOPS above 3 per GB and for backup storage, not just capacity.
- **You have HPC, analytics or media rendering in the same storage conversation** → FSx, where Lustre and the other file system options reach millions of IOPS. A general-purpose file server is the wrong tool for that job.
- **You want one predictable invoice and have the ops capacity to run the box** → a dedicated server, where $79.00/mo buys 32 GB of RAM, 1 TB of NVMe and 30 TB of transfer with nothing metered.

Two things to confirm before any order: whether your data is allowed to sit in the provider's region at all, and who owns the backup and the OS licence at 2 a.m. when something breaks. Everything else is sizing.

👉 [Start with SpinServers' current dedicated server and VPS listings](https://bit.ly/Spinservers)
