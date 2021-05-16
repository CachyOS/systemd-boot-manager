# systemd-boot Manager for Manjaro

This projects attempts to add automation for users of systemd-boot with Manjaro.  It has 3 components.

##### 1. A shell script which provides the following functionality
  * Installs and configures systemd-boot
  * Generate entries based on installed kernels and a series of options described below
  * Removes entries for kernels no longer installed
  * Updates systemd-boot
##### 2. A series of alpm hooks that are called to automate the process
##### 3. A configuration file to support a variety of use cases described below

### Usage
While the script is primarily intended to automated via the provided hooks, it can also be invoked manually as follows:
```
Usage: sdboot-manage [action]

Actions:
  gen     generates entries for systemd-boot based on installed kernels
  remove  removes orphaned systemd-boot entries
  setup   installs systemd-boot and generate initial entries
  update  updates systemd-boot
```

### Filesystem Support
The script was tested for basic functionality in the following root filesystem configurations:
* btrfs
* ext4
* f2fs
* zfs
* ext4 on luks
* ext4 on lvm on luks
* ext4 on luks on lvm

I don't know of any reason it wouldn't support every filesystem that manjaro-architect supports with the exception of ntfs.  Hopefully people are not using ntfs as their root fs.

### Configuration
The configuration file is located at `/etc/sdboot-manage.conf`.  The displayed options are the defaults and it has the following structure.
```
# config file for sdboot-manage

# kernel options to be appended to the "options" line
#LINUX_OPTIONS=""
#LINUX_FALLBACK_OPTIONS=""

# the DEFAULT_ENTRY option determines if and how the default entry in loader.conf should be managed
#   "latest"    The most recent Manjaro kernel will be used(the one with the highest version number)
#   "oldest"    The oldest Manjaro kernel will be used(the one with the lowest version number)
#   "manual"    Don't modify the default setting
#DEFAULT_ENTRY="latest"

# ENTRY_ROOT is a template that describes the beginning of the name for system-boot entries
# The ENTRY_ROOT will be followed by the kernel version number
# For example, if ENTRY_ROOT="manjaro" and you are using kernel 4.19 your entry will be named "manjaro4.19.conf"
#ENTRY_ROOT="manjarolinux"

# setting REMOVE_EXISTING to "yes" will remove all your existing systemd-boot entries before building new entries
#REMOVE_EXISTING="yes"

# unless OVERWRITE_EXISTING is set to "yes" existing entries for currently installed kernels will not be touched
# this setting has no meaning if REMOVE_EXISTING is set to "yes"
#OVERWRITE_EXISTING="no"

# when REMOVE_OBSOLETE is set to "yes" entries for kernels no longer available on the system will be removed
#REMOVE_OBSOLETE="yes"

# if PRESERVE_FOREIGN is set to "yes", do not delete entries starting with $ENTRY_ROOT
#PRESERVE_FOREIGN="no"

# setting NO_AUTOUPDATE to "yes" will stop the updates to systemd-boot when systemd is updated - not recommended unless you are seperately updating systemd-boot
#NO_AUTOUPDATE="no"

# setting NO_AUTOGEN to "yes" will stop the automatic creation of entries when kernels are installed or updated
#NO_AUTOGEN="no"
```

Notes:
* Hibernation into a swapfile on BTRFS is not currently supported.
