# ossim-vagrant-ansible
ansible build examples for ossim and o2 development builds.

We supplied a working example that can be used to instantiate a developement environment and build for the entire o2 and ossim baseline found under ossimlabs

## Required dependencies

You must install the following on your host system.
 
 * vagrant
 * Virtualbox
 * ansible

These are available as packages on most systems.  

## Setup and Configuration

The next step will take a while to run and install the necessary packages:

```
git clone https://github.com/ossimlabs/ossim-vagrant-ansible.git
cd ossim-vagrant-ansible/o2-dev
vagrant up
```

You should see the import of the Centos/7 box and the startup of the OS and then the ansible configuration of all the packages.  sdkman will be installed with using the ansible-sdkman role.  We imported the code found here: [https://github.com/Comcast/ansible-sdkman.git](https://github.com/Comcast/ansible-sdkman.git) into our project

Groovy, grails, and gradle will be installed by the ansible-sdkman role.

Once all packages are installed you should be abel to do:

```
vagrant ssh
./build-ossim.sh
```
