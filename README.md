# iOS6 Cydia Repo

# How to update

## Build a `deb` package (This is a demo)

### Install packages

```bash
sudo apt install dpkg-dev
```

### Build

```bash
mkdir -p package/DEBIAN
mkdir -p package/usr/bin
```

### Create file `package/usr/bin/hello`

```bash
#!/bin/sh
echo "Hello Cydia"
```

### chmod

```
chmod +x package/usr/bin/hello
```

### Create control file

`package/DEBIAN/control`:

```deb
Package: com.yourname.helloios6
Name: Hello iOS6
Version: 1.0
Architecture: iphoneos-arm
Description: A test package for iOS 6 Cydia
Maintainer: YourName
Section: Utilities
Priority: optional
```

### Build `deb`

```bash
dpkg-deb --build package # Not work for armv7
dpkg-deb -Zgzip -b ./package_folder package.deb # For armv7 (no zst)
```

## Put into repo

```bash
mv xxx.deb repo-root/debs/tw.xym.xxx.deb
dpkg-scanpackages [PATH] [OVERRIDE] > Packages
dpkg-scanpackages repo-root/debs/ /dev/null > Packages
bzip2 -k Packages
```