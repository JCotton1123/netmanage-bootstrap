# Netmanage Bootstrap

Use the contents of this repo to **bootstrap or upgrade an instance of [NetManage](https://github.com/JCotton1123/netmanage)**. For now the virtual machine(s) must be running a variant of RHEL (RHEL, CentOS, etc).

If you'd like to quickly demo NetManage, the [Vagrant install option](#option-1---vagrant) will get an instance of NetManage, infrastructure and application, up and running quickly.

## Setup

### Pre install/upgrade

* Edit `group_vars/all` to your liking
* If upgrading, take a backup of your database with `mysqldump -u <user> -p netmanage > netmanage.sql` and store this somewhere safe.

### Install/upgrade

#### Option 1 - Vagrant:

Fast and easy, use [Vagrant](https://www.vagrantup.com/) to setup a single multi-function (app and db) instance for hosting NetManage. The included Vagrantfile will configure the instance with a public interface (bridged) which is typically required to accept incoming connections such as log messages and tftp uploads.

#### Option 2 - Ansible:

Use [Ansible](http://docs.ansible.com/) and the included configuration to setup a single multi-function instance, or separate application and database instances.

* Edit `hosts` if you'd like to use separate servers for hosting the application and database.
* Install the EPEL repo `rpm -i http://fedora-epel.mirror.lstn.net/6/i386/epel-release-6-8.noarch.rpm`
* Install ansible `sudo yum -y install ansible`
* Start the orchestration `ansible-playbook -i hosts site.yml`

## Post setup

### First Install

* Verify you can log into NetManage web interface using the server name (`apache_server_name`) you configured in `group_vars/all`. The default username and password is `admin` and `netmanage`.
* Configure any *online settings* within the NetManage web interface under *Settings*.
* Setup regular backups of the NetManage database, usually `mysqldump -u app_netmanage --password=<password> netmanage > netmanage.sql`, and store them in a safe location.

## To Do

* Figure out a better way to handle the firewall configurations
* Look into a better password generation solution
