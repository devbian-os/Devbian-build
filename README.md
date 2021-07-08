#dev
A Debian live ISO that auto-executes eReuse.org Workbench when
booting communicating with an eReuse.org Workbench Server.

## Usage
### Requirements
We use [debian-live](https://live-team.pages.debian.net/live-manual/html/live-manual/index.en.html) to build the ISO. So 
[install it](https://live-team.pages.debian.net/live-manual/html/live-manual/installation.en.html).
In Debian it is just `sudo apt install live-build`.

### Build an ISO
Execute (from [here](https://live-team.pages.debian.net/live-manual/html/live-manual/the-basics.en.html#167)): 
```bash
    git clone https://github.com/eReuse/workbench-live.git
    cd workbench-live
    # Note you can pass parameters to lb config to alter the ISO
    sudo lb build
```

### Speed up building
You can speed up downloads considerably if you use a local mirror. [...] 
Set the default for your build system in `/etc/live/build.conf`. 
Simply create this file and in it, set the corresponding `LB_MIRROR_*` variables to your preferred mirror. 
All other mirrors used in the build will be defaulted from these values." For example:

```bash
LB_MIRROR_BOOTSTRAP="http://ftp.caliu.cat/debian/" 
LB_MIRROR_CHROOT_SECURITY="http://security.debian.org/" 
LB_MIRROR_CHROOT_BACKPORTS="http://ftp.caliu.cat/debian/"
```

You can execute a package like `netselect-apt` to know which mirror is the fastest for you.

## Modify the contents
Read 
[the debian-live manual](https://live-team.pages.debian.net/live-manual/html/live-manual/index.en.html)
as we followed it to build this.

### Overview
The structure is as follows:
- `auto/config`: Generic build options like architecture.
- `config/bootloaders/isolinux`: Bootloader params.
- `config/includes.chroot/opt/workbench`: Skeleton where Devbian files will be placed into
  the final ISO (at path `/opt/workbench`).
- `config/includes.chroot/home/user`: The home dir of the user the live uses. We add `.zshrc` for the theme

### Commit
Before committing, ensure you execute `sudo lb clean` just a cautious measure.


### Problem resolution
- If you cancel the `lb build` you won't be able to delete some `chroot` stuff because they are mounted. Just reboot
  and try with `sudo`.
- If you perform changes, try to use `lb clean --purge` to ensure a deep cleaning.
