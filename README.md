# Debian image builder for local tests

Configuration script is copied from [multani/packer-qemu-debian](https://github.com/multani/packer-qemu-debian). 
Thx a lot for this template to configure cloud-image to be ran locally easily.

## Execute

If you have any errors with packer or terraform please install the dependencies :
```bash
❯ packer init .
❯ terraform init
```

To run the image :
```bash
❯ packer build debian.pkr.hcl
...
==> Wait completed after 7 minutes 24 seconds

==> Builds finished. The artifacts of successful builds are:
--> qemu.debian: VM files in directory: output
--> qemu.debian: VM files in directory: output

❯ terraform apply -auto-approve
... 
Apply complete! Resources: 3 added, 0 changed, 0 destroyed.

Outputs:

ip = "10.0.100.XXX"
```

A VM is booted with the image built with packer, you can connect with `debian:debian` on the output ip by terraform.

```
❯ ssh debian@10.0.100.XXX
debian@10.0.100.XXX's password:
Linux localhost 5.10.0-11-amd64 #1 SMP Debian 5.10.92-1 (2022-01-18) x86_64
__    _                                              _      _      
| |  | |                       /\                   | |    (_)     
| |__| |_   _  __ _  ___      /  \   _ __ ___   __ _| |_ __ _  ___ 
|  __  | | | |/ _` |/ _ \    / /\ \ | '_ ` _ \ / _` | | '__| |/ __|
| |  | | |_| | (_| | (_) |  / ____ \| | | | | | (_| | | |  | | (__ 
|_|  |_|\__,_|\__, |\___/  /_/    \_\_| |_| |_|\__,_|_|_|  |_|\___|
              __/ |                                               
              |___/      

debian@localhost:~$
```