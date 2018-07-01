# Zaloni Data Platform Ansible Based Installer.

(BETA. For Zaloni internal use only.)

This is an Ansible based installer for ZDP. See [the wiki](https://wiki.zaloni.net/index.php/Ansible_based_installer_for_ZDP) for details.

## Prerequisites

1. Install Ansible from [their website](http://docs.ansible.com/ansible/latest/intro_installation.html).
2. Clone this repository.
3. Ensure the target nodes have python 2.6 (or above) and sshd installed already.
4. Optional: set up passwordless SSH between your ansible machine and the target nodes.
5. Install pyYAML on the target machines (yum install -PyYAML).


## Configuring hosts

Please edit the <code>inventory/hosts.yml</code> file and make appropriate changes.

The various playbook.yml files describe the various roles for each host.

## Roles

TODO: fix me

Here is a list of important roles you can use

0. prerequistes : checks if all the prerequisites needed for various services are all installed. Doesnt install anything
1. install : installs all the zdp services
2. backup : back up all the data
3. enable-ssl : enables https/TLS/SSL across all the services
4. remove : uninstalls zdp from listed hosts
5. start : starts the services in the correct order
6. stop : performs a safe shut down
7. restore.yml : back up all the data
8. Upgrade: performs an upgrade. This is not a rolling upgrade. However, each daemon is upgraded and restarted after the othe other so if you have

## Playbooks

TODO: fix me

Here's a common set of sample playbooks you can run:

NOTE- DO not pass any argument for "Kerberos username [XXXX]: Kerberos password for  :

## Appendix: Ansible crash course

1. Install ansible using "brew install ansible" on OS-X or "yum install ansible" on Linux

2. cd core/zaloni-bedrock-deploy-scripts/src/ansible

3. List out all the hosts in your playbook
<code>
ansible all -i inventory/hosts.yml --list-hosts
</code>

4. Run a command <code>df -h</code> as bbdeka on all the hosts
<code>
ansible all -i inventory/hosts.yml -u bbdeka -m command -a "df -h"
</code>
(If you dont have password-less ssh setup, append the <code>--ask-pass</code> to this command)

5. Run a command <code>df -h</code> as sudo on all the hosts
<code>
	ansible all -i inventory/hosts.yml  -m command -a "df -h" --ask-pass -become
</code>
(If sudo requires a password, append the <code>-K</code> to this command)

6. Dry-run a playbook on the hosts:
<code>
ansible-playbook -C zdp-install-playbook.yml -i inventory/single-node-example --ask-pass
</code>

7. Run the playbook 
<code>
ansible-playbook zdp-installer-playbook.yml -i inventory/single-node-example
</code>