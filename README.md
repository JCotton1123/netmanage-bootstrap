# Netmanage Bootstrap

Use the contents of this repo to setup NetManage from scratch.

## Install

* Clone this repo
* Edit the configurations within group_vars/all.
* Edit `hosts` if you'd like to use separate servers for hosting the application and database.
* Install the EPEL repo `rpm -i http://fedora-epel.mirror.lstn.net/6/i386/epel-release-6-8.noarch.rpm`
* Install ansible `sudo yum -y install ansible`
* Start the orchestration `ansible-playbook -i hosts site.yml`
