Game & Watch Ghidra Export
==========================
This repo contains an export of the Ghidra database I've been using while
reverse engineering the Game & Watch: Super Mario Bros,' firmware. It has
both internal and external flash mapped, along with a bunch of symbols for
things I've looked at.

To use this, you will first need to supply bits of the firmware (put it alongside
the .xml file):

- `int_flash.bin`: Internal flash firmware, 128KiB
- `ext_flash_decrypted.bin`: External flash data, only the used parts, which is
  1,005,680 bytes. Make sure it's decrypted too. You may obtain this from
  dumping starting at `0x90000000` after the Game & Watch has booted.
- `itcm_rwdata.bin`: Decompressed ITCM RAM data
- `dtcm_rwdata.bin`: Decompressed DTCM RAM data

For the latter two files, use [this snippet](https://gist.github.com/GMMan/be54eff20731cbe4aba6756fd459349e)
to decompress. You will need to point it to `0x180a4` in the internal flash to
decompress ITCM RAM data and `0x180b4` for DTCM RAM data.

Note the XML export is lossy, so you'll be missing local variable names. I plan
on looking into Ghidra's ZIP export format to see if I can exclude the binary
and allow import using your own dumped firmware.
