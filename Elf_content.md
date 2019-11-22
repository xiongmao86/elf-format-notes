## Program Interpreter Segment 
file offset = 0x02a8
file size = 0x1c
from 0x02a8 to 0x02c3

### xxd
``` xxd
000002a0:                     2f6c 6962 3634 2f6c          /lib64/l
000002b0: 642d 6c69 6e75 782d 7838 362d 3634 2e73  d-linux-x86-64.s
000002c0: 6f2e 3200                                o.2.............
```

### content
"/lib64/ld-linux-x86-64.so.2"

## Auxiliary Information -- Note Segment
file offset = 0x02c4
file size = 0x44
from 0x02c4 to 0x0307

### xxd
```xxd
000002c0:           0400 0000 1000 0000 0100 0000      ............
000002d0: 474e 5500 0000 0000 0300 0000 0200 0000  GNU.............
000002e0: 0000 0000 0400 0000 1400 0000 0300 0000  ................
000002f0: 474e 5500 908e 3568 7fa5 9656 02bf 4f89  GNU...5h...V..O.
00000300: e0eb 58e4 244f 0050                      ..X.$O.P
```

### Field Information
`n_namesz` word
`n_descsz` word
`n_type` word interpretion depend on other options in Elf file.
`name` length `n_namesz`
`desc` length `n_descsz`

### Entry 
`n_namesz` = 0x 0400 0000 = 4
`n_descsz` = 0x 1000 0000 = 0x10 = 16
`n_type` = 0x 0100 0000 = 1 
`name` = 'GNU\0'
`desc` = 0x 0000 0000 0300 0000 0200 0000 0000 0000 ???

### Entry 2
`n_namesz` = 0x 0400 0000 = 4
`n_descsz` = 0x 1400 0000 = 0x14 = 20
`n_type` = 0x 0300 0000 = 0x03 = 3
`name` = 'GNU\0'
`desc` = 0x908e 3568 7fa5 9656 02bf 4f89 0eeb 58e4 244f 0050 ???
