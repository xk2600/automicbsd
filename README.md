# automicbsd project

Currently we have various ways that things get configured in the bsd world. Currently, when
using remote tooling such as Ansible, Puppet, Salt, Chef and the likes each creates its own
module to update configurations throughout the filesystem and environment in FreeBSD. This
leads to different approaches depending on who wrote the module as we in the BSD world
don't currently have all the necessary tooling in place to allow multiple modifications of
all the components.

This project seeks to make available tooling and libraries to simplify common modifications
to the system.

# System Configuration Locations and Types


## Common modifications required

System boot configuration:

- `/boot/loader.conf`
- `/etc/sysctl.conf`
- persistent `/etc/rc.conf` via `/usr/sbin/sysrc`

Daemon specific startup files:

- `/etc/rc.d/`
- `/usr/local/etc/rc.d/`

Application and General System configuration files are stored in the root `etc` folder as 
well as within `/local` when the application is sourced from `pkg` or the ports tree.
Sometimes, the application supports breakout into discrete component files usually stored
in a directory with the `.d` suffix.

- `/etc/*.conf`
- `/etc/*.conf.d/*`
- `/usr/local/etc/*.conf`
- `/usr/local/etc/*.conf.d/*`

Other common tasks:

- Package management via `/usr/sbin/pkg` (or `/usr/sbin/pkgsrc`)
- Port compilation and installation via `Makefile` in `/usr/ports`
- User creation via `user add`


## Ancillary tasks

Not necissarily in scope but oculd be useful/important and therefore noted:

#### storage management

- `/sbin/geom` CLASS tools: `/sbin/gpart`, `/sbin/geli`, `/sbin/gmirror`. etc.
- filesystem creation via newfs
- memory disk management via `/sbin/mdconfig`
- zpool, zvol, and zfs management via `/sbin/zpool` and `/sbin/sfs`tools.
- mounting of filesystems with `/sbin/(u)mount` and `/sbin/zfs (u)mount` commands

#### network management

- interface control via `/sbin/ifconfig`
- forwarding/routing control via `sbin/route`
- firewall control via `/sbin/pfctl`, `/sbin/ipf`, or `/sbin/ipfw`

#### hardware mangement

- `/sbin/camcontrol`
- `/sbin/conscontrol`
- `/sbin/nvmecontrol`
- swap control via `/sbin/swapon` and `/sbin/swapoff`
- update next boot environment with: `/sbin/nextboot`



# 

## Current Approaches

- by hand
- appended to with `/bin/cat >> someconfigfile.conf`
- custom awk/sed scripts
- (abuse of) `/usr/bin/sysrc` script, for example `/usr/bin/sysrc -f /boot/loader.conf`
- live update of system with custom scripts at boot: 
  - change kernel environment with: `/


##

- by hand
- appended to with `/bin/cat >>`

