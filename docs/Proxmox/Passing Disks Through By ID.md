# Passing Disks Through By ID

This is sometimes necessary if the HBA is on the same IOMMU group as other hardware which causes the system to kernel panic and reboot when the VM is booted.

```bash
# Command to list all disks
ls -l /dev/disk/by-id
```

```bash
# Command to pass through disks
qm set <VM ID> -sata# /dev/disk/by-id/<disk name>

# Example commands
qm set 101 -sata0 /dev/disk/by-id/ata-WDC_WD40EFRX-68WT0N0_WD-WCC4E2ZRHC7Z
qm set 101 -sata1 /dev/disk/by-id/ata-WDC_WD40EFRX-68WT0N0_WD-WCC4E2REE2T6
qm set 101 -sata2 /dev/disk/by-id/ata-WDC_WD40EFRX-68WT0N0_WD-WCC4E2ZRHUXK
qm set 101 -sata3 /dev/disk/by-id/ata-WDC_WD40EFRX-68WT0N0_WD-WCC4E3TV5LR5
qm set 101 -sata4 /dev/disk/by-id/ata-APS-SL3N-240_SK18C41134WL
```