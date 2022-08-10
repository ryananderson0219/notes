# [![Proxmox Virtual Environment](https://proxmox.com/images/proxmox/Proxmox_logo_standard_hex_400px.png)](https://proxmox.com/en/proxmox-ve)

## Introduction
Proxmox VE is a complete, open-source server management platform for enterprise virtualization. It tightly integrates the KVM hypervisor and Linux Containers (LXC), software-defined storage and networking functionality, on a single platform. With the integrated web-based user interface you can manage VMs and containers, high availability for clusters, or the integrated disaster recovery tools with ease.

The enterprise-class features and a 100% software-based focus make Proxmox VE the perfect choice to virtualize your IT infrastructure, optimize existing resources, and increase efficiencies with minimal expense. You can easily virtualize even the most demanding of Linux and Windows application workloads, and dynamically scale computing and storage as your needs grow, ensuring that your data center adjusts for future growth.

## Knowledgebase

### Increase a VM Disk Size
> After you increase the size of the disk in Proxmox, you need to resize the disk in the guest VM.
> - LVM
>   - `pvresize /dev/vda{#}`
>   - `lvextend /dev/mapper/root -l+100%FREE`
>   - `resize2fs /dev/mapper/root` (ext2/3/4) -OR- `xfs_growfs /dev/mapper/root` (XFS)
>
> - Non-LVM
>   - `lsblk`
>   - If necessary (`sudo apt -y install cloud-guest-utils gdisk`)
>   - `growpart /dev/vda {#}`
>   - `lsblk` (check)
>   - `resize2fs /dev/vda{#}`

### Cluster Management
> - Change quorate votes
> - `pvecm expected {#}`
>
> - Cluster Status
>  - `pvecm status`
>
> - Delete Node from Cluster
>  - List nodes from another node `pvecm nodes`
>  - Shutdown node to be removed from cluster
>  - Delete Node from same node as first step - `pvecm delnode {NODE NAME}`
> **Do NOT power on the deleted node while connected to network**
