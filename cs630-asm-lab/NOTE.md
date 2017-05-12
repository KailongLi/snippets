# NOTE

## Chapter 15 & 17

### Compile manydot.s on 64bit hosts

    $ as --32 res/manydots.s -o res/manydots.o
    $ ld -m elf_i386 res/manydots.o -o res/manydots
    $ ./res/manydots
    How many dots do you want to see? 10
    ..........
    $

### Using hello.s and try32bit.s

- hello.s

        $ as --32 res/hello.s -o res/hello.o
        $ ld -m elf_i386 res/hello.o -o res/hello
        $ res/hello

- hello.s + try32bit.s:

        $ ./configure res/try32bit.s
        $ make
        $ dd if=res/hello.o of=pmboot.img seek=13
        $ make pmboot

### Compile loadmap.cpp in gentoo 64bit

    $ g++ -m32 loadmap.cpp -o loadmap

- Why gentoo? because, in ubuntu 64bit and debian 64bit, it can not find the
suitable libstdc++, the `ld` not work normally. even if do not have gentoo,
do not worry, can use `-S` with readelf or `-h` with objdump instead of loadmap
to get the map of hello.o.

- In lesson 17, the basic procedure is the same, just need to substitute
try32bit.s as trydebug.s

## Chapter 19

If want to run hello in elfexec.s, the memory given to qemu should more
than 128M for the text and data section of hello will be copied to 0x08048000
and 0x08049000 which is more than 128M, so in qemu.sh we use.

        qemu-system-i386 -m 129M -fda $image -boot a

## Chapter 23 and later?

If want to support smp with qemu, can use the -smp options.
