# Intro
This section describes how to create a [Docker Swarm mode](https://docs.docker.com/engine/swarm/) environment in a [Virtualbox](https://www.virtualbox.org/)
- One Swarm manager node
- Three Swarm worker nodes

The idea is to create a suitable Swarm mode environt locally for testing purpose where an Apache Solr cluster could be deployed

## Prerequisites _(Optional)_
The Vagrantfile in thhis repo creates an environment that deploys a Docker Swarm mode cluster. It is assumed:
- The user has admin privileges on the machine where this cluster is being deployed
- At least 12GB of free RAM is available on that machine. Otherwise, Vagrantfile will need editing to adjust the available memory
  - `v.customize ["modifyvm", :id, "--memory", <MEMORY_ALLOCATION>]`
- Latest version of [Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads) is installed
- Latest version of [Git](https://git-scm.com/downloads) is installed
- Latest version of [Vagrant](https://www.vagrantup.com/intro/getting-started/install.html) is installed
  - Install Vagrant Host Manager plugin by running the following command in your commandline terminal. This plugin updates the host files on both guest and host machines:
    - `vagrant plugin install vagrant-hostmanager`
  - Install vagrant-vbguest plugin by running the following command:
    - `vagrant plugin install vagrant-vbguest`

## Vagrant Box provisioning
  1. Launch the guest machine:
      1. `clear && vagrant up --color` _(you might get asked for your system password as the local hostfile will need to be updated)_
  2. Should you have a need to SSH to vagrant box then run the following commands:
      1.  `vagrant ssh`
      2. `cd /vagrant` _(this is a mount point for the files on the host machine)_
      3. `docker node ls` _(this will confirm the numbber of nodes)_

## Vagrant Box teardown
Once finished, run the following command:
  - `vagrant destroy --force`