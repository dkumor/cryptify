# cryptify

Python script that allows using files as mounted encrypted filesystems, similarly to truecrypt's file containers.

Since cloud server providers oftentimes don't have the option of encrypting the disk, `cryptify` is a script that lets you use a file to encrypt your data instead.

It requires sudo access.

## How to use it

First, create an encrypted container which has 10GB space in the file `mycontainer.crypt`

```bash
./cryptify create mycontainer.crypt 10G
```

You can then mount it at folder `mountpoint` with the following:

```bash
./cryptify open mycontainer.crypt ./mountpoint
```

At this point you can put whatever files you want inside mountpoint, and they will be written to the encrypted file.

Then, when done:

```bash
./cryptify close mycontainer.crypt
```

to safely unmount.

## Dependencies

Modern ubuntu should have these installed by default, but if on a custom distro, you will need cryptsetup, and `mkfs.ext4`

```bash
sudo apt-get install cryptsetup
```

## All options

```
usage: Sets up and runs LUKS containers [-h] [-u USER] [--root ROOT]
                                        {create,open,close} cryptfile
                                        [mountpoint_or_size]

positional arguments:
  {create,open,close}   What to do?
  cryptfile             the encrypted data file
  mountpoint_or_size    Mountpoint of container in open, size in create
                        (ignored in close)

optional arguments:
  -h, --help            show this help message and exit
  -u USER, --user USER  The user name to open as
  --root ROOT           Can cryptify be run as root?

```
