# ossim-vagrant-ansible
ansible build examples for ossim and o2 development builds.

We supplied a working example that can be used to instantiate a developement environment and build for the entire o2 and ossim baseline found under ossimlabs

## Required dependencies

You must install the following on your host system. At the time of writing this document the version are listed next to the packages.
 
 * vagrant (2.x)
 * Virtualbox (5.2.X)
 * ansible (2.5.3)

These are available as packages on most systems.  

## Setup and Configuration

The next step will take a while to run and install the necessary packages:


```
git clone https://github.com/ossimlabs/ossim-vagrant-ansible.git
cd ossim-vagrant-ansible/o2-dev
vagrant up
```

**WARNING** At the time of writing this document we had a problem with a link on the cloud serving up the boxes.  If you get an error that states some kind of 404 then you can download the centos/7 box manually and then rerun the **vagrant up** command.  Only do this if the vagrant up fails with a 404.  You can replace it with a later version that does not have a broken link:

```
vagrant box add --box-version 1803.01 centos/7
select virtual box number and then hit return and then it will start downloading
```

With a successful execution of the **vagrant up** command you should see the import of the Centos/7 box and the startup of the OS and then the ansible configuration of all the packages.  sdkman will be installed via using the ansible-sdkman role.  We imported the code found here: [https://github.com/Comcast/ansible-sdkman.git](https://github.com/Comcast/ansible-sdkman.git) into our project and will adhere to its licensing.  All other code will adhere to the MIT License and is free to use and modify.

Groovy, grails, and gradle will be installed by the ansible-sdkman role.

Once the vagrant box is configured for the first time you will need to run the commands to configure a dev database and a prod database:

```
psql -c 'create database "omardb-1.9.0-dev"'
psql -c 'create extension postgis' -d omardb-1.9.0-dev
psql -c 'create database "omardb-1.9.0-prod"'
psql -c 'create extension postgis' -d omardb-1.9.0-prod
```

Once all packages are installed you should be able to do:

```
vagrant ssh
./build-ossim.sh
```

Once finished, for the first time through we will make sure that the local.properties is there for the joms build:

```
cd ossim-oms/joms
cp local.properties.template local.properties 
ant clean mvn-install
```


Note:  when you **vagrant ssh** into the machine it will automatically source the build environment and will have all necessary variables defined such as the O2_DEV_HOME, REPOSITORY_MANAGER_URL, OSSIM_INSTALL_PREFIX, ... etc for building the ossim and the OMAR distributions. 

