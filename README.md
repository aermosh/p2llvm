************************************************************************

p2llvm project for Fedora 37 

p2llvm release:
https://github.com/ne75/p2llvm/releases/tag/v0.6

loadp2 from flexprop release:
https://github.com/totalspectrum/flexprop/releases/tag/v5.9.23

***************************************************************************

1. Download p2llvm.tar.gz and unzip it into /opt (so that it’s /opt/p2llvm): 

sudo tar -xvzf p2llvm.tar.gz -C /opt

***************************************************************************

2. Dowload hello_world directory and check if everyhting works correctly:

cd hello_world
make

***************************************************************************

If P2 (propeller 2) is connected to your USB port then output should look something like this:

rm -rf ./build
mkdir -p build
/opt/p2llvm/bin/clang -Os --target=p2 -o build/hello_world_p2llvm.o -c hello_world_p2llvm.cpp
/opt/p2llvm/bin/clang: /lib64/libtinfo.so.6: no version information available (required by /opt/p2llvm/bin/clang)
/opt/p2llvm/bin/clang --target=p2 -Wl,--gc-sections -o build/hello_world_p2llvm.elf build/hello_world_p2llvm.o
/opt/p2llvm/bin/clang: /lib64/libtinfo.so.6: no version information available (required by /opt/p2llvm/bin/clang)
/opt/p2llvm/bin/ld.lld: /lib64/libtinfo.so.6: no version information available (required by /opt/p2llvm/bin/ld.lld)
/opt/p2llvm/bin/loadp2 -v -ZERO -b 2000000 -t -FIFO 1024 build/hello_world_p2llvm.elf
trying /dev/ttyUSB0...
P2 version G found on serial port /dev/ttyUSB0
Setting load mode to CHIP
Setting clock_mode to 12427f8
Loading fast loader for chip...
Sending header
Loading build/hello_world_p2llvm.elf - 507904 bytes
chksum: ad OK
( Entering terminal mode.  Press Ctrl-] or Ctrl-Z to exit. )

Hello World from p2llvm!

***************************************************************************

If no P2 is connected or found then output will look like this:

rm -rf ./build
mkdir -p build
/opt/p2llvm/bin/clang -Os --target=p2 -o build/hello_world_p2llvm.o -c hello_world_p2llvm.cpp
/opt/p2llvm/bin/clang: /lib64/libtinfo.so.6: no version information available (required by /opt/p2llvm/bin/clang)
/opt/p2llvm/bin/clang --target=p2 -Wl,--gc-sections -o build/hello_world_p2llvm.elf build/hello_world_p2llvm.o
/opt/p2llvm/bin/clang: /lib64/libtinfo.so.6: no version information available (required by /opt/p2llvm/bin/clang)
/opt/p2llvm/bin/ld.lld: /lib64/libtinfo.so.6: no version information available (required by /opt/p2llvm/bin/ld.lld)
/opt/p2llvm/bin/loadp2 -v -ZERO -b 2000000 -t -FIFO 1024 build/hello_world_p2llvm.elf
Could not find a P2
make: *** [Makefile:28: load] Error 1

****************************************************************************
 
3. To load your program into flash memory of P2 use this command:

/opt/p2llvm/bin/loadp2 -v -t -b 2000000 -FIFO 1024 "@0=/opt/p2llvm/loaders/P2ES_flashloader.bin,@8000+build/hello_world_p2llvm.elf"

****************************************************************************
