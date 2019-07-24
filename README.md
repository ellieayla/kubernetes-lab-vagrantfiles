Deploy 6 vms for use in Kubernetes The Hard Way.

 controller-0
 controller-1
 controller-2
 worker-0
 worker-1
 worker-2


# Setup Vagrant

Install VMware OVFTOOL: https://www.vmware.com/support/developer/ovf/ and ensure `ovftool` or `ovftool.exe` is in your `PATH`

Install Vagrant: https://www.vagrantup.com/downloads.html

```
vagrant version
```

Install Vagrant ESXi Plugin:

```
vagrant plugin install vagrant-vmware-esxi
vagrant plugin list
```

# Use it

```
vagrant up
vagrant status
vagrant ssh-config
```
