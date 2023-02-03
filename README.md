# MariaDB replication playground

The sole purpose of this repo is to quickly setup two local Virtualbox VMs with
Rockylinux8 and configure them using Ansible to be MySQL primary and replica
server to have a playground to learn and play with MariaDB.

The environment features two servers:

* db1 (192.169.2.5) - configured as a MariaDB primary server
* db2 (192.168.2.6) - configured as a MariaDB replica server connected to the above primary

## Installation

The following is required if you want to use the vagrant provisioner to setup
local VMs:

* [Virtualbox](https://www.virtualbox.org)
* [Vagrant](https://vagrantup.com)

But you can run the Ansible stuff on any hosts. Just use any other inventory
file.

Configuration is done using Ansible. If you do not have a respective environment
the repository features a `Pipfile` to install the tools using `pipenv`

The following should be enough to get everything up and running.

```
cd playground_mysqlrepl
pipenv shell
pipenv sync
vagrant up
```

## Usage

Two servers are setup and configured with Ansible automatically when spinning up
the VMs with `vagrant up`.

Using `vagrant ssh db1` or `vagrant ssh db2` lets you connect to either of the
two VMs. By default host `db1` will be configured as the primary server and
`db2` as a replication replica server.

Look into `playbook/db/main.yml` for the details.

You can manually run ansible anytime again using `ansible-playbook -i
inventories/vagrant/inventory.ini configure.yml` in the project's top-level
directory or by simply running `vagrant provision`.
