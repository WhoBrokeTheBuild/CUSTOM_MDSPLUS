CUSTOM_MDSPLUS

Skeleton "MDSPLUS" distribution. The content isn't important, the concept is:

- traditional ACQ400 packages are delivered as .tgz and unzipped into RAM
 - nice and simple, but wastes valuable RAM as package becomes large

- new scheme delivers a package as a filesystem imag.


Files stored at /mnt/packages/NN-package_name-version-*.img shall be

0. A filesystem image. squashfs is recommended.

1. Automatically mounted in sequence on boot. The mount point shall be autocreated as:
/usr/local/package-name
The packages are mounted BEFORE the normal ".tgz" RAM packages.

2. If a file named /usr/local/package-name/package-name.init exists, it's executed immediately after mount.

3. The FS is mounted read-only. If there needs to local customisation, then the can be handled using an
overlay. The file name should be modified to:
/mnt/ko/NN-package_name-version-*.oly

then the package image is mounted as the readonly part of the image, while a directory
/mnt/local/package/package_name is created as the writable part of the image.
overlayfs combines the two as a unified image at /usr/local/package-name
This doesn't really break the "no writes to the SD" image, provided it's only one-time init data. 
