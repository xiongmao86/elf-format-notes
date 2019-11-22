## Elf Program Header Table
### xxd binary format
$ sed -n 5,43p hw.binary # 0040 - 02a7
```xxd
00000040: 0600 0000 0400 0000 4000 0000 0000 0000  ........@.......
00000050: 4000 0000 0000 0000 4000 0000 0000 0000  @.......@.......
00000060: 6802 0000 0000 0000 6802 0000 0000 0000  h.......h.......
00000070: 0800 0000 0000 0000 0300 0000 0400 0000  ................
00000080: a802 0000 0000 0000 a802 0000 0000 0000  ................
00000090: a802 0000 0000 0000 1c00 0000 0000 0000  ................
000000a0: 1c00 0000 0000 0000 0100 0000 0000 0000  ................
000000b0: 0100 0000 0400 0000 0000 0000 0000 0000  ................
000000c0: 0000 0000 0000 0000 0000 0000 0000 0000  ................
000000d0: 6005 0000 0000 0000 6005 0000 0000 0000  `.......`.......
000000e0: 0010 0000 0000 0000 0100 0000 0500 0000  ................
000000f0: 0010 0000 0000 0000 0010 0000 0000 0000  ................
00000100: 0010 0000 0000 0000 bd01 0000 0000 0000  ................
00000110: bd01 0000 0000 0000 0010 0000 0000 0000  ................
00000120: 0100 0000 0400 0000 0020 0000 0000 0000  ......... ......
00000130: 0020 0000 0000 0000 0020 0000 0000 0000  . ....... ......
00000140: 5801 0000 0000 0000 5801 0000 0000 0000  X.......X.......
00000150: 0010 0000 0000 0000 0100 0000 0600 0000  ................
00000160: b82d 0000 0000 0000 b83d 0000 0000 0000  .-.......=......
00000170: b83d 0000 0000 0000 5802 0000 0000 0000  .=......X.......
00000180: 6002 0000 0000 0000 0010 0000 0000 0000  `...............
00000190: 0200 0000 0600 0000 c82d 0000 0000 0000  .........-......
000001a0: c83d 0000 0000 0000 c83d 0000 0000 0000  .=.......=......
000001b0: f001 0000 0000 0000 f001 0000 0000 0000  ................
000001c0: 0800 0000 0000 0000 0400 0000 0400 0000  ................
000001d0: c402 0000 0000 0000 c402 0000 0000 0000  ................
000001e0: c402 0000 0000 0000 4400 0000 0000 0000  ........D.......
000001f0: 4400 0000 0000 0000 0400 0000 0000 0000  D...............
00000200: 50e5 7464 0400 0000 1420 0000 0000 0000  P.td..... ......
00000210: 1420 0000 0000 0000 1420 0000 0000 0000  . ....... ......
00000220: 3c00 0000 0000 0000 3c00 0000 0000 0000  <.......<.......
00000230: 0400 0000 0000 0000 51e5 7464 0600 0000  ........Q.td....
00000240: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000250: 0000 0000 0000 0000 0000 0000 0000 0000  ................
00000260: 0000 0000 0000 0000 1000 0000 0000 0000  ................
00000270: 52e5 7464 0400 0000 b82d 0000 0000 0000  R.td.....-......
00000280: b83d 0000 0000 0000 b83d 0000 0000 0000  .=.......=......
00000290: 4802 0000 0000 0000 4802 0000 0000 0000  H.......H.......
000002a0: 0100 0000 0000 0000
```

### Field information
#### `p_type` type of segment
```C
/* Legal values for p_type (segment type).  */

#define	PT_NULL		0		/* Program header table entry unused */
#define PT_LOAD		1		/* Loadable program segment */
#define PT_DYNAMIC	2		/* Dynamic linking information */
#define PT_INTERP	3		/* Program interpreter */
#define PT_NOTE		4		/* Auxiliary information */
#define PT_SHLIB	5		/* Reserved */
#define PT_PHDR		6		/* Entry for header table itself */
#define PT_TLS		7		/* Thread-local storage segment */
#define	PT_NUM		8		/* Number of defined types */
#define PT_LOOS		0x60000000	/* Start of OS-specific */
#define PT_GNU_EH_FRAME	0x6474e550	/* GCC .eh_frame_hdr segment */
#define PT_GNU_STACK	0x6474e551	/* Indicates stack executability */
#define PT_GNU_RELRO	0x6474e552	/* Read-only after relocation */
#define PT_LOSUNW	0x6ffffffa
#define PT_SUNWBSS	0x6ffffffa	/* Sun Specific segment */
#define PT_SUNWSTACK	0x6ffffffb	/* Stack segment */
#define PT_HISUNW	0x6fffffff
#define PT_HIOS		0x6fffffff	/* End of OS-specific */
#define PT_LOPROC	0x70000000	/* Start of processor-specific */
#define PT_HIPROC	0x7fffffff	/* End of processor-specific */
```
#### `p_flags` flags
```C
/* Legal values for p_flags (segment flags).  */

#define PF_X		(1 << 0)	/* Segment is executable */
#define PF_W		(1 << 1)	/* Segment is writable */
#define PF_R		(1 << 2)	/* Segment is readable */
#define PF_MASKOS	0x0ff00000	/* OS-specific */
#define PF_MASKPROC	0xf0000000	/* Processor-specific */
```
#### `p_offset` `p_vaddr` `p_paddr`
file offset
virtual address
physical address
#### `p_filesz` `p_memsz`
size in file
size in memory
#### `p_align` = alignment

### Segments
#### Program Header Table
`p_type` = 0x 0600 0000
`p_flags` = 0x 0400 0000 readable
`p_offset` = `p_vaddr` = `p_paddr` = 0x 4000 0000 0000 0000
`p_filesz` = `p_memsz` = 0x 6802 0000 0000 0000 = 0x0268 = 616
`p_align` = 0x 0800 0000 0000 0000 = 8

#### Program Interpreter
`p_type` = 0x 0300 0000 
`p_flags` = 0x 0400 0000 readable
`p_offset` = `p_vaddr` = `p_paddr` = 0x a802 0000 0000 0000 = 0x02a8
0x02a8 = 0x40(previous segment offset) + 0x0268(previous segment file size)
`p_filesz` = `p_memsz` = 0x 1c00 0000 0000 0000 = 0x1c
`p_align` = 0x 0100 0000 0000 0000 = 1

#### Loadable Program Segment
`p_type` = 0x 0100 0000
`p_flags` = 0x 0400 0000
`p_offset` = `p_vaddr` = `p_paddr` = 0x 0000 0000 0000 0000
`p_filesz` = `p_memsz` = 0x 6005 0000 0000 0000 = 0x0560
`p_align` = 0x 0010 0000 0000 0000 = 0x1000

#### Loadable Program Segment 2
`p_type` = 0x 0100 0000
`p_flags` = 0x 0500 0000 readable and executable
`p_offset` = `p_vaddr` = `p_paddr` = 0x 0010 0000 0000 0000 = 0x1000
`p_filesz` = `p_memsz` = 0x bd01 0000 0000 0000 = 0x01bd
`p_align` = 0x 0010 0000 0000 0000 = 0x1000

#### Loadable Program Segment 3
`p_type` = 0x 0100 0000
`p_flags` = 0x 0400 0000
`p_offset` = `p_vaddr` = `p_paddr` = 0x 0020 0000 0000 0000 = 0x2000
`p_filesz` = `p_memsz` = 0x 5801 0000 0000 0000 = 0x0158
`p_align` = 0x 0010 0000 0000 0000 = 0x1000

#### Loadable Program Segment 4
`p_type` = 0x 0100 0000
`p_flags` = 0x 0600 0000 readable and writable
`p_offset` = 0x b82d 0000 0000 0000
`p_vaddr` = `p_paddr` = 0x b83d 0000 0000 0000
`p_filesz` = 0x 5802 0000 0000 0000 = 0x0258
`p_memsz` = 0x 6002 0000 0000 0000 = 0x0260
`p_align` = 0x 0010 0000 0000 0000 = 0x1000

#### Dynamic Linking Information
`p_type` = 0x 0200 0000 = 0x02 Dynamic 
`p_flags` = 0x 0600 0000 = 0x06 readable and writable
`p_offset` = 0x c82d 0000 0000 0000 = 0x2dc8
`p_vaddr` = `p_paddr` = 0x c83d 0000 0000 0000 = 0x3dc8
`p_filesz` = `p_memsz` = 0x f001 0000 0000 0000 = 0x01f0
`p_align` = 0x 0800 0000 0000 0000 = 8

#### Auxiliary Information
`p_type` = 0x 0400 0000 = 0x04 Note
`p_flags` = 0x 0400 0000 = 0x04 readable
`p_offset` = `p_vaddr` = `p_paddr` = 0xc402 0000 0000 0000 = 0x02c4
`p_filesz` = `p_memsz` = 0x 4400 0000 0000 0000 = 0x44
`p_align` = 0x 0400 0000 0000 0000 = 4

#### GCC EH FRAME Segment
`p_type` = 0x 50e5 7464 = 0x 6474 e550 `GNU_EH_FRAME`
`p_flags` = 0x 0400 0000 = 0x04 readable
`p_offset` = `p_vaddr` = `p_paddr` = 0x 1420 0000 0000 0000 = 0x2014
`p_filesz` = `p_memsz` = 0x 3c00 0000 0000 0000 0000 = 0x3c
`p_align` = 0x 0400 0000 0000 0000 = 4

#### GNU Stack
`p_type` = 0x 51e5 7464 = 0x 6474e551 `GNU_STACK`
`p_flags` = 0x 0600 0000 readable and writable
`p_offset`= `p_vaddr` = `p_paddr` =`p_filesz` = `p_memsz` = 0x 0000 0000 0000 0000 = 0
`p_align` = 0x 1000 0000 0000 0000 = 0x10

#### GNU Relocation
`p_type` = 0x 52e5 7464 = 0x 6474 e552 `GNU_RELRO`
`p_flags` = 0x 0400 0000 readable
`p_offset` = 0x b82d 0000 0000 0000 = 0x2db8
`p_vaddr` = `p_paddr` = 0x b83d 0000 0000 0000 = 0x3db8
`p_filesz` = `p_memsz` = 0x 4802 0000 0000 0000 = 0x0248
`p_align` = 0x 0100 0000 0000 0000 0000 = 1
