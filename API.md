# Tables
The Usable PayLoad Format provides a couple of means to pass information on
to the OS and payloads.

## Code Execution
Usable & Effective Firmware passes control to a payload or OS in form of a
SELF binary, ceasing control over the platform.

## coreboot table
Named after the project that originally designed it, the coreboot table is
an extensible data structure providing the information gathered by Usable &
Effective Firmware to payloads and operating systems.

FIXME: describe how to search for the table correctly.

The table header looks like this:

```c
struct lb_header
{
        uint8_t  signature[4]; /* LBIO */
        uint32_t header_bytes;
        uint32_t header_checksum;
        uint32_t table_bytes;
        uint32_t table_checksum;
        uint32_t table_entries;
};
```

Every entry in the boot enviroment list will correspond to a boot info record.
Encoding both type and size.  The type is obviously so you can tell what it is.
The size allows you to skip that boot enviroment record if you don't know
what it easy.  This allows forward compatibility with records not yet defined.

```c
struct lb_record {
        uint32_t tag;           /* tag ID */
        uint32_t size;          /* size of record (in bytes) */
};
```


##  Entry Types
```c
#define LB_TAG_UNUSED           0x0000
#define LB_TAG_MEMORY           0x0001
#define LB_TAG_HWRPB            0x0002
#define LB_TAG_MAINBOARD        0x0003
#define LB_TAG_VERSION          0x0004
#define LB_TAG_EXTRA_VERSION    0x0005
#define LB_TAG_BUILD            0x0006
#define LB_TAG_COMPILE_TIME     0x0007
#define LB_TAG_COMPILE_BY       0x0008
#define LB_TAG_COMPILE_HOST     0x0009
#define LB_TAG_COMPILE_DOMAIN   0x000a
#define LB_TAG_COMPILER         0x000b
#define LB_TAG_LINKER           0x000c
#define LB_TAG_ASSEMBLER        0x000d
// 0x000e is used by device tree entry?
#define LB_TAG_SERIAL           0x000f
#define LB_TAG_CONSOLE          0x0010
#define LB_TAG_CMOS_OPTION_TABLE 200

#define LB_TAG_OPTION 201
#define LB_TAG_OPTION_ENUM 202
#define LB_TAG_OPTION_DEFAULTS 203
#define LB_TAG_OPTION_CHECKSUM 204
```
