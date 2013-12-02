xen-tools-4.1.4-patched-qemu
============================

Patched Xen-tools 4.1.4 binaries, qemu memory leak

Compiled from patch https://gist.github.com/bivald/7691087 on:

niklas@unstable:~$ uname -r
3.2.0-4-amd64
niklas@unstable:~$ cat /etc/debian_version 
7.2

For background, read http://markmail.org/message/gseh3dw3tkcyjohm#query:+page:1+mid:ashwwh6epljmbweb+state:results

1. Install dependencies
For me, this was..
apt-get install libsdl1.2debian libpixman-1-0 libgl1-mesa-glx

ln -s /home/niklas/qemu-patched-binaries/libblktap.so.3.0 /usr/lib/libblktap.so.3.0
ln -s /home/niklas/qemu-patched-binaries/libxenctrl.so.4.0 /usr/lib/libxenctrl.so.4.0
ln -s /home/niklas/qemu-patched-binaries/libxenguest.so.4.0 /usr/lib/libxenguest.so.4.0

2. Check that the qemu-dm actually works:
/home/niklas/qemu-patched-binaries/qemu-dm

Should give same output as /usr/lib/xen-4.1/bin/qemu-dm

3. Install the qemu-dm (move the old, link the new)
mv /usr/lib/xen-4.1/bin/qemu-dm /usr/lib/xen-4.1/bin/qemu-dm.none-patched
ln -s /home/niklas/qemu-patched-binaries/qemu-dm /usr/lib/xen-4.1/bin/qemu-dm