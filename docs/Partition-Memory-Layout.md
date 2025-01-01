# Partition and Memory Layout

## Memory Layout Table

| Offset                | Size           | MTD Name | UBIFS Name | Contents                             |
|-----------------------|----------------|----------|------------|--------------------------------------|
| 0x000000000000        | 0x000000100000 | 1 MiB    | u-boot     | u-boot (env at offset 0x40000, size 0x20000) |
| 0x000000100000        | 0x000000400000 | 4 MiB    | uImage     | Kernel image                         |
| 0x000000500000        | 0x00001fb00000 | 507 MiB  | root       | Root file system                     |
| **Total**             | **0x000020000000** | **512 MiB** |            |                                      |

## Description of Sections

1. **u-boot (1 MiB)**
    - **Offset:** `0x000000000000`
    - **Description:** This is the U-Boot bootloader, with environment variables stored at offset `0x40000` and a size of `0x20000`.
  
2. **uImage (4 MiB)**
    - **Offset:** `0x000000100000`
    - **Description:** The kernel image (`uImage`), used by the bootloader to boot the system.

3. **Root Filesystem (507 MiB)**
    - **Offset:** `0x000000500000`
    - **Description:** The root filesystem, which contains the entire operating system and applications.

## Total Memory Usage

- **Total Size:** 512 MiB
