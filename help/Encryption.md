### Εncryption

When a new project is created with **"rftool create ProjectName"** a new rfboot .hex file is created
with a unique RF channel, SyncWord, and XTEA key. These paramaters are stored in the FLASH (inside the hex file)
and NOT in the eeprom.

The idea of encryption emerged as a way to learn some things about encryption. The AES
cipher resulted in an oversized bootloader, more than the 4Kb limit of atmega328 so XTEA
is used because is very small and the code in wikipedia is in public domain by the
algorithm creators.

The use of encryption may seem overkill . Who cares to steal the firmware from the air, you may ask.
In most cases the answer is nobody.
But for a commercial project this can be a concern, and encryption offers peace in mind.

And it turns out,  even for a completely open
source project the use of encryption is essential. The reason is that without encryption,
the bootloader can easily be fooled to upload any code -by anyone- in the RF module's distance range.
This can be done on purpose or even accidentally, if for example someone (or you) try to upload
code to another module.

Notice how different are bootloaders such as optiboot or atmegaboot.
They don't need encryption, because code is transfered by wire, and
physical access to the module is required.

I found that encryption is not slowing down the uploading process.
It is also transparent to the user, so it does not complicate the upload process.

For these reasons encryption is permanently enabled in rfboot. If for some reason you need
to disable encryption you have to edit the source code.

The firmware is uploaded to the atmega328 encrypted with XTEA algorithm in CBC mode.
As rfboot selects a different IV at every session, even if we upload the same file several times,
the data on the air will be different every time. An "attacker" cannot use an old recorded
session, and cannot send random data either, because rfboot checks if the first
packet is encrypted with the correct XTEA key and the chosen IV. The IV is stored
in the flash (Not the EEPROM) and uses 2 bytes. Only the first 65536 uploads will have unique IV's. This is OK
as the FLASH can be written reliably only 10000 times.

The firmware is not encrypted in the atmega flash. When the bootloader is first installed with
"make isp", the fuses are set so an ISP programmer cannot read the FLASH
neither the EEPROM,
but I have no solid information if atmega328 can withstand FLASH/EEPROM read attacks.

There is also the possibility that rfboot has some bug, and an exploit can trick it to
reveal the code somehow. Or that the data are badly encrypted and can easily decrypted, and so on.

Generally speaking, no warranties that the code works, offers any security, confidentiality,
it is useful to any particular purpose, etc.
