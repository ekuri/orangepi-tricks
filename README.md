# SBC-tricks

## Running x86_64 docker

1. Install qemu user static

```bash
sudo apt install qemu-user-static
```

3. Install binfmt-support

```bash
sudo apt install binfmt-support
```

2. check if x86_64 binfmt is registered

```bash
update-binfmts --display
```

which should show you something like

```
qemu-x86_64 (enabled):
     package = qemu-user-static
        type = magic
      offset = 0
       magic = \x7f\x45\x4c\x46\x02\x01\x01\x00\x00\x00\x00\x00\x00\x00\x00\x00\x02\x00\x3e\x00
        mask = \xff\xff\xff\xff\xff\xfe\xfe\xfc\xff\xff\xff\xff\xff\xff\xff\xff\xfe\xff\xff\xff
 interpreter = /usr/bin/qemu-x86_64-static
    detector =
```

4. run ubuntu22.04 x64 image

```bash
$ docker run -it --rm --platform linux/amd64 ubuntu:22.04 uname -m
x86_64
```

> other platform should be also supported, check you qemu-*-static

```bash
$ ls /usr/bin/qemu-*-static
/usr/bin/qemu-aarch64_be-static  /usr/bin/qemu-microblazeel-static  /usr/bin/qemu-or1k-static        /usr/bin/qemu-sh4-static
/usr/bin/qemu-aarch64-static     /usr/bin/qemu-microblaze-static    /usr/bin/qemu-ppc64abi32-static  /usr/bin/qemu-sparc32plus-static
/usr/bin/qemu-alpha-static       /usr/bin/qemu-mips64el-static      /usr/bin/qemu-ppc64le-static     /usr/bin/qemu-sparc64-static
/usr/bin/qemu-armeb-static       /usr/bin/qemu-mips64-static        /usr/bin/qemu-ppc64-static       /usr/bin/qemu-sparc-static
/usr/bin/qemu-arm-static         /usr/bin/qemu-mipsel-static        /usr/bin/qemu-ppc-static         /usr/bin/qemu-tilegx-static
/usr/bin/qemu-cris-static        /usr/bin/qemu-mipsn32el-static     /usr/bin/qemu-riscv32-static     /usr/bin/qemu-x86_64-static
/usr/bin/qemu-hppa-static        /usr/bin/qemu-mipsn32-static       /usr/bin/qemu-riscv64-static     /usr/bin/qemu-xtensaeb-static
/usr/bin/qemu-i386-static        /usr/bin/qemu-mips-static          /usr/bin/qemu-s390x-static       /usr/bin/qemu-xtensa-static
/usr/bin/qemu-m68k-static        /usr/bin/qemu-nios2-static         /usr/bin/qemu-sh4eb-static
```

> More about qemu-user: https://wiki.debian.org/QemuUserEmulation
