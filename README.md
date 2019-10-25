# Vagrant Demo
This Vagrant setup installs 3 CentOS 7 machines, 1 saltmaster and 2 saltminions. This setup can be used to develop salt states or can be used for workshops etc.

## Prerequisites
This setup has been tested on Ubuntu 18.04 LTS. The following prerequisites are needed:
- Vagrant 2.2.6
- virtualbox 6.0
- virtualbox extension pack (https://download.virtualbox.org/virtualbox/6.0.14/Oracle_VM_VirtualBox_Extension_Pack-6.0.14.vbox-extpack)

## How to use
After you installed the prerequisites you can start using the environment by following the steps underneath.

```bash
git clone https://github.com/haijeploeg/salt-demo.git
cd salt-demo
vagrant up
```

After vagrant up has setup the environment you can start developing your states in the states directory and developing your pillar data in the pillar directory. There is no need to develop in the virtual machines that Vagrant justs created. The states and pillar directory are being syned to the saltmaster. So you can use your favorite editor on your environment!

| NOTE: All Vagrant commands need to be executed from the root of the salt-demo directory, where the Vagrant file is. |
| --- |

### SSH
To ssh into one of the three vagrant boxes you can use the vagrant ssh command. First checkout which names the virtual machines have.

```bash
user@laptop:~/salt-demo$ vagrant status
Current machine states:

master                    not created (virtualbox)
minion1                   not created (virtualbox)
minion2                   not created (virtualbox)

This environment represents multiple VMs. The VMs are all listed
above with their current state. For more information about a specific
VM, run `vagrant status NAME`.
```

To ssh into the saltmaster:

```bash
vagrant ssh master
```

To ssh into one of the minions:

```bash
vagrant ssh minion1
```

### Destroying the environment
If you are done, or you want a clean environment, you can destroy the Vagrant environment.

```bash
vagrant destroy -f
```