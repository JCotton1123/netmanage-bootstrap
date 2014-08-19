# Netmanage Bootstrap

Use the contents of this repo to bootstrap an instance of [NetManage](https://github.com/JCotton1123/netmanage). For now the virtual machine(s) must be running a variant of RHEL (RHEL, CentOS, etc).

## Setup

### Pre install

Regardless of which option you use to bootstrap NetManage, `group_vars/all` contains the configurable variables for the setup process. Edit this file as necessary.

### Install

#### Option 1 - Vagrant:

Fast and easy, use [Vagrant](https://www.vagrantup.com/) to setup a single multi-function (app and db) instance for hosting NetManage. The included Vagrantfile will configure the instance with a public interface (bridged) which is typically required to accept incoming connections such as log messages and tftp uploads. 

#### Option 2 - Ansible:

* Edit `hosts` if you'd like to use separate servers for hosting the application and database.
* Install the EPEL repo `rpm -i http://fedora-epel.mirror.lstn.net/6/i386/epel-release-6-8.noarch.rpm`
* Install ansible `sudo yum -y install ansible`
* Start the orchestration `ansible-playbook -i hosts site.yml`

### Post install

The bootstrap process does not handle loading a schema although in the future I plan on adding support for handling schema upgrades.

If you're bootstrapping a new instance of NetManage:

* Clone this repo onto the database server
* Load the schema, `mysql -u root netmanage < Config/Schema/init.sql`

## Post setup

Once complete, you should be able to log into the NetManage interface using the url you configured. The default username and password is `admin` and `netmanage`. The final step is to set appropriate settings for your network under `Settings`.
