**Pre-config**

1. Install VirtualBox
2. Install Vagrant
3. Install latest python2
4. Install python-pip
5. Install ansible

**How to manage VM**

`vagrant up - create VM and run provision`

`vagrant provision - re run provision`

`vagrant destroy  - stops and  delete VM`

`vagrant ssh - ssh into a host`

**How to run without vagrant**

`ansible-playbook -i inventory/<environment> deploy-es-<environment>.yaml --ask-pass --ask-become-pass`
