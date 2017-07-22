This fork of the original VeraCrypt 1.21 release version (9 July 2017) is modified for testing out the ability to load containers from arbitrary offsets. This version is Windows only.

Just to be very clear, this version should be considered to be more of a hack than anything else. Consider a warning. That said, it seems to work fine under certain scenarios. In the current implementation the offset feature is only supported with mount operations on files. The GUI works as normal otherwise. To use the offset feature you must use the commandline with /i and pass an offset in decimal notation. The value of offset must be sector size aligned (usually 512 bytes).

General Note
-Be aware that these binaries are incompatible with the legacy binaries.
-A special procedure is required to prepare the containers. See below.
-The binaries are signed with test certificate, which means you must configure TESTSIGNING ON in the bcd on 64-bit.

Tested OS
-Tested on fully updated Windows 7 and 10 as of 8 July 2017.
-On 32-bit it just works as is.
-On 64-bit you need to configure TESTSIGNING ON in the boot configuration with bcdedit.exe. That is because 64-bit Windows since Vista require a driver to be properly signed in order to load it. And my files are only signed with a test certificate.

About special containers
Here's a collection of some tools to fascilitate the creation of the special containers; https://github.com/jschicht/MakeContainer

Steps
1. Run the VeraCrypt wizard and create a container. Don't put anything inside it yet.
2. Run any the tools in this collection to hide the container in some other file. A bat file will be generated with an example command line for loading it later on.
3. Run the patched VeraCrypt with a command like the one specified in the example bat file that was generated in step 2. Now you will have to format the the volume once more after it is decrypted. This is because the physical offset changed. When the volume is formatted the second time, it is ready for use. This is the same for both standard and hidden volumes.
4. Make sure the host file that contains the hidden container does not get modified at the offsets where the container bytes are stored. Static files are of cource safest to use, but is for instance possible to store the container inside a text based logfile as long as all new log entries are written to EOF and the logfile is not recycled.

Source modifications
The places where the source code is modified are all marked with a //Joakim comment. The affected files are;
Common\Apidrvr.h
Common\Dlgcode.c
Common\Dlgcode.h
Common\Format.c
Common\Tcdefs.h
Driver\Ntdriver.c
Driver\Ntdriver.h
Driver\Ntvol.c
ExpandVolume\ExpandVolume.c
Format\Tcformat.c
Mount\Mount.c

Download binaries
https://github.com/jschicht/VeraCrypt/releases


