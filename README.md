# edi-qemu

Setup to reproduce QEMU/systemd tight loop.

## Preparation

Prior to using this configuration you have to install edi
according to [this instructions](https://docs.get-edi.io/en/latest/getting_started.html).

Once edi is installed and this configuration cloned,
a container can be generated using the following command:

``` bash
sudo edi -v lxc configure qemu-buster qemu-buster.yml
```

## Problem Description

Please note that systemd and journalctl within the container eat 100% CPU time each.

The affected container can be entered as follows

``` bash
lxc exec qemu-buster bash
```

Within the container the following command shows the tight loop:

``` bash
qemu-aarch64-static --strace /bin/systemctl status
```

It looks like systemd is stuck here:

``` bash
2837 getsockopt(3,1,31,274891889456,274887218756,274888927920) = -1 errno=34 (Numerical result out of range)
2837 getsockopt(3,1,31,274891889456,274887218756,274888927920) = -1 errno=34 (Numerical result out of range)
2837 getsockopt(3,1,31,274891889456,274887218756,274888927920) = -1 errno=34 (Numerical result out of range)
2837 getsockopt(3,1,31,274891889456,274887218756,274888927920) = -1 errno=34 (Numerical result out of range)
```





