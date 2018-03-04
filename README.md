# Notes on Running LXD on Alpine

+ Boot option and sysctl config [Reference](https://forum.alpinelinux.org/forum/pax-grsecurity/unprivileged-lxc-and-grsecurity-kernel)
  + Kernel Option config in /etc/update-extlinux.conf `grsec_sysfs_restrict=0` 
    + run update-extlinux and reboot
  + If you can't run lxd exec on your container and are getting `error: EOF`
    + sysctl:
      ```
      kernel.grsecurity.chroot_caps = 0
      kernel.grsecurity.chroot_deny_chmod = 0
      kernel.grsecurity.chroot_deny_pivot = 0
      kernel.grsecurity.chroot_deny_chroot = 0
      kernel.grsecurity.chroot_deny_mount = 0
      ```

+ Based on [issue #4141](https://github.com/lxc/lxd/issues/4141)
  + There is something wrong with alpine's newuidmap/newgidmap
  + Fix: 
    ```
    chmod -x /usr/bin/newuidmap
    chmod -x /usr/bin/newgidmap
    ```
