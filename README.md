# cryptify
Python script allowing for simple creation/mounting of encrypted containers

## Dependencies
```bash
sudo apt-get install python-subprocess32 cryptsetup
```



## What it does

dm-crypt allows using files as mounted encrypted filesystems, similarly to truecrypt's file containers.

Since VPS providers oftentimes don't have the option of encrypting the disk, `cryptify` is a simple shell which
allows you to easily set up an encrypted folder on your system.

It requires sudo access.


## How to use it

First, create an ext4 encrypted container which has 10GB space in the file `foldercrypt`

```bash
./cryptify --size 10000 create
```

On future reboots, when the container already exists, you can just run:
```bash
./cryptify open
```

At this point you have a `foldercrypt.crypt` file, which is mounted at the `foldercrypt` folder.

Then, when done with the folder, simply run
```bash
./cryptify close
```

to safely unmount.

## All options

```
$./cryptify --help
usage: Sets up and runs LUKS containers [-h] [-i CONTAINER] [-o MOUNTPOINT]
                                        [-s SIZE] [-u USER]
                                        command

positional arguments:
  command               create,open,close

optional arguments:
  -h, --help            show this help message and exit
  -i CONTAINER, --container CONTAINER
                        The container to hold encrypted data in
  -o MOUNTPOINT, --mountpoint MOUNTPOINT
                        The mountpoint of the container
  -s SIZE, --size SIZE  The size of the container in megabytes
  -u USER, --user USER  The user name to mount as

```
