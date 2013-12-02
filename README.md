xen-tools-4.1.4-patched-qemu
============================

Patched Xen-tools 4.1.4 binaries for qemu memory leak. This repo is just to keep the binaries in case someone else needs them after reading the **entire threads** on http://markmail.org/message/gseh3dw3tkcyjohm#query:+page:1+mid:ashwwh6epljmbweb+state:results and http://lists.nongnu.org/archive/html/qemu-devel/2012-12/msg03677.html

You probably don't need this. This is more for historical sake and my own reference.

Compiled on a:

	niklas@unstable:~$ uname -r
	3.2.0-4-amd64
	niklas@unstable:~$ cat /etc/debian_version 
	7.2`


How to install the patched binaries
-------------------------------------------------
1. Install dependencies. For me, this was..

		apt-get install libsdl1.2debian libpixman-1-0 libgl1-mesa-glx
		ln -s /home/niklas/qemu-patched-binaries/libblktap.so.3.0 /usr/lib/libblktap.so.3.0
		ln -s /home/niklas/qemu-patched-binaries/libxenctrl.so.4.0 /usr/lib/libxenctrl.so.4.0
		ln -s /home/niklas/qemu-patched-binaries/libxenguest.so.4.0 /usr/lib/libxenguest.so.4.0

2. Check that the qemu-dm actually works:

	`/home/niklas/qemu-patched-binaries/qemu-dm`

	Should give same output as `/usr/lib/xen-4.1/bin/qemu-dm` 

3. Install the qemu-dm (move the old, link the new), something like this:

		mv /usr/lib/xen-4.1/bin/qemu-dm /usr/lib/xen-4.1/bin/qemu-dm.none-patched
		ln -s /home/niklas/qemu-patched-binaries/qemu-dm /usr/lib/xen-4.1/bin/qemu-dm

How the binaries was produced
--------------------------------------------
	git clone git://xenbits.xen.org/xen.git
	cd xen
	git checkout tags/RELEASE-4.1.4
	make dist-tools #downloads qemu from git, not sure if needed?
	---applied patch https://gist.github.com/bivald/7691087 here ----
	make dist-tools