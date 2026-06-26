Absolutely. I actually think this is worth documenting properly because there are a lot of GA36/R36S owners who end up with the same questions. I'll write it as a **professional step-by-step guide** based on the exact process we followed. Later, we can turn it into a PDF with screenshots and annotations.

---

# Complete Guide: Backing Up and Migrating a GA36/R36S Firmware to a New SD Card

> **Device Used**
>
> * Console: GA36 / R36S Clone
> * Board: **GA36-MB V1.1-20251025**
> * Original Firmware: **GA36-UDT-ARKOS-TF-R-20260321**
> * New SD Card: **SanDisk Ultra 64 GB A1**
> * Operating System: Windows 11

---

# Tools Required

| Tool                  | Purpose                                  |
| --------------------- | ---------------------------------------- |
| Win32 Disk Imager     | Backup and restore entire SD card        |
| DiskGenius            | View partitions and expand ROM partition |
| OSFMount *(optional)* | Mount `.img` backup for inspection       |
| 7-Zip *(optional)*    | Extract compressed firmware images       |

---

# Part 1 – Create a Backup of the Original SD Card

## Step 1

Power off the console.

Remove the **TF1 (OS)** SD card.

Insert it into your PC.

---

## Step 2

Open **Win32 Disk Imager** as **Administrator**.

---

## Step 3

Select an image file location, for example:

```text
C:\Users\<username>\Documents\R36S Project\imagebkp-original.img
```

---

## Step 4

Choose the SD card drive letter.

Example:

```text
Device:
E:
```

---

## Step 5

Ensure:

* Read Only Allocated Partitions = **Unchecked**

---

## Step 6

Click:

```text
Read
```

Wait until the backup completes.

Expected backup size:

Approximately **31 GB** (for a 32 GB SD card).

---

## Step 7

Store the backup safely.

Example project structure:

```text
R36S Project
│
├── imagebkp-original.img
├── Original SD Card
├── Firmware
└── Notes
```

---

# Part 2 – Restore the Backup to a New SD Card

Insert the new **64 GB SanDisk Ultra**.

---

## Step 1

Open **Win32 Disk Imager**

---

## Step 2

Select

```text
imagebkp-original.img
```

---

## Step 3

Choose the **64 GB SD card**

Example

```text
Device:
E:
```

Verify carefully before proceeding.

---

## Step 4

Click

```text
Write
```

A warning will appear:

> Writing to a physical device can corrupt the device.

This is normal.

Click **Yes**.

---

## Step 5

Wait until the write finishes.

Do **not** interrupt the process.

---

## Step 6

Windows may ask:

> You need to format the disk before using it.

Choose:

```text
Cancel
```

Never format Linux partitions.

---

# Part 3 – Verify the Partition Layout

Open **DiskGenius**.

Expected layout:

```text
Disk 2

Linux      1.61 GB
Boot       32 MB
ROMs       27.68 GB
Free Space 30.18 GB
```

This confirms the image was restored successfully.

---

# Part 4 – Expand the ROM Partition

The restored image only uses the original card's capacity.

The remaining space must be added to the ROM partition.

---

## Step 1

Right-click the **27.68 GB FAT32 partition**.

Select

```text
Resize Partition
```

---

## Step 2

Drag **only the RIGHT edge** of the partition until:

```text
Keep Unallocated = 0 B
```

Expected new size:

Approximately

```text
57.87 GB
```

---

## Step 3

Click

```text
Start
```

---

## Step 4

Approve the pending operation.

DiskGenius updates the partition table.

---

## Step 5

Wait until:

```text
Completed Successfully
```

---

# Part 5 – Boot Test

Safely eject the SD card.

Insert it into:

```text
TF1 (Right Slot)
```

Leave TF2 empty.

Power on.

Expected result:

* Boots normally
* Games appear
* Saves preserved
* Larger ROM partition available

---

# Result

Original:

```text
Boot
Linux
27 GB ROMs
```

After migration:

```text
Boot
Linux
58 GB ROMs
```

---

# Recovery

Always keep:

* Original SD card
* imagebkp-original.img

Never overwrite either.

If the new card fails, simply insert the original card and continue playing.

---

# Lessons Learned

* Always create a full image backup before experimenting.
* Use **Win32 Disk Imager** for sector-by-sector cloning.
* Use **DiskGenius** to expand the FAT32 ROM partition.
* Ignore Windows prompts to format Linux partitions.
* Keep the original SD card as a permanent recovery card.

---

# Current Status

| Task                      | Status     |
| ------------------------- | ---------- |
| Backup original firmware  | ✅ Complete |
| Restore to 64 GB SanDisk  | ✅ Complete |
| Expand ROM partition      | ✅ Complete |
| Verify boot               | ✅ Complete |
| Preserve original SD card | ✅ Complete |

---

