# Ansible ARTiMED Galaxy instance
Deploys a Galaxy instance on the host machine. 
It includes Galaxy with postgresql database. 
To deploy just download the ansible-artimed/galaxy_vm/install.sh file and run:
```
#Download ansible-artimed/galaxy_vm/install.sh and execute:
bash install.sh;
```

Note that the minimum requirements are a OpenSSH client, Ansible >=1.8 and git.

# Ansible ARTiMED Virtual Machine
Ansible playbooks for ARTiMED Virtual Machine
Deploys ARTiMED Vagrant box (the virtual machine). It includes Galaxy with postgresql database. To deploy just download the ansible-artimed/galaxy_vm/install_vm.sh file and run:
```
#Download ansible-artimed/galaxy_vm/install_vm.sh and execute:
bash install_vm.sh;
```

The install_vm.sh file will:
 - verify the requirements (git, pip, virtualenv, ansible, vagrant, virtualbox, ...).
 - create the installation directory for the Vagrant box ($HOME/ansible-artimed/galaxy_vm/).
 - git clone this galaxy server playbook for vagrant provision procedure.
 - do a vagrant up to deploy the box.
 - start galaxy
 - install the tools listed in into Galaxy
 
Note that the minimum requirements are a OpenSSH client, Ansible >=1.8, Vagrant >=1.7.4, Virtual Box (compatible with vagrant - see vagrant site) and git. 

# Running Galaxy VM from the host machine 
Galaxy is installed as a SO service, however if you want to run galaxy from the host machine as a shell application, open another shell on host machine on the same install directory (ansible-artimed/galaxy_vm) and execute:
```
vagrant ssh -c "sudo service galaxy stop"
vagrant ssh -c "sudo -i -u galaxy sh /home/galaxy/galaxy/run.sh"
```

# Re-doing
If you want to redo the installation process "cd" to the box directory (where the Vagrantfile is) and do the following steps:
```
vagrant package --output backup.box #backup your box;
vagrant destroy #it will destroy completelly your box, so do not miss the previous command;
vagrant up;
```

FYI, this repository has submodules, so to clone it with the roles "git clone --recursive" command must be always used.
Galaxy is configured to run on the default port (8080), to monitor all network cards and the admin user is artimed@gmail.com. 
Galaxy database is labeled as galaxy with owner galaxy.
