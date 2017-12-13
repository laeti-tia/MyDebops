My Generic ansible/debops skeleton
==================================

This is my ansible/debops skeleton for starting any Debian/Ubuntu host management automation.  It is heavily based on the very useful repository of Ansible roles customised for Debian/Ubuntu administration: [debops][debops].

Usage
-----

I usually run this as follows:

    debops ansible/playbooks/bootstrap.yml
    debops ansible/playbooks/general.yml

When I only need to update the users setup:

    debops ansible/playbooks/general.yml --tags role::general_users

When I only need to update and add new packages/soft:

    debops ansible/playbooks/general.yml --tags role::general_install

Customisation
-------------

You'll generally want to augment this setup by:

- adding some roles in `roles/`
- adding more variables in `inventory/group_vars` or `inventory/host_vars`
- adding more playbooks

But this is all ansible/debops usage after that.

Creation
--------

This setup has been created from a generic `debops-init .` and some customisation of

- the `.debops.cfg`
- a sample `inventory/hosts` file
- 2 generic playbooks
    - one to bootstrap ansible/debops to my liking: `playbooks/bootstrap.yml`
    - one to configure my default setup on my hosts: `playbooks/general.yml`
- some defaults variables in `inventory/group_vars/all/`

debops specifics on MacOS
-------------------------

I'm running this setup from a MacOS box.  Under (High) Sierra (10.12 and 10.13) I had to do the following to make debops work properly:

    brew install bash
    pip2 install ansible==2.3.2
    pip2 install debops
    debops-update
    sudo ln -s ~/Library/Application\ Support/debops /usr/local/share/debops
    brew install encfs
    brew install caskroom/cask/osxfuse

This is because ansible/debops only works with bash 4 and ansible < 2.4.  See also the [task_src not found][task_src] error and the config in my `debops.cfg` file.


[debops]: https://github.com/debops/debops
[task_src]: https://github.com/carlalexander/debops-wordpress/wiki/Known-issues
