# Audit Setup

Role that setup the [audit](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/security_guide/sec-starting_the_audit_service) service using the security guidelines established by the [CIS Benchmark for RHEL 7](http://cisecurity.org) over the **4.1 Configure System Accounting (auditd)** section.

> It uses the `augenrules` command, which is disable by default in RHEL 6.

## Requirements

This role was created using [Ansible 2.9](https://docs.ansible.com/ansible/2.9/) for macOS and tested using the [centos/7](https://app.vagrantup.com/centos/boxes/7) boxes for [Vagrant v.2.2.6](https://www.vagrantup.com/docs/index.html) with [VirtualBox](https://www.virtualbox.org/) as a Provider.

The [Ansible modules](https://docs.ansible.com/ansible/2.9/modules/modules_by_category.html) used in the role are:

- [yum](https://docs.ansible.com/ansible/2.9/modules/yum_module.html#yum-module) - requires Python 2 and `yum` (for Python 3 see [dnf](https://docs.ansible.com/ansible/2.9/modules/dnf_module.html#dnf-module));
- [copy](https://docs.ansible.com/ansible/2.9/modules/copy_module.html#copy_module)
- [template](https://docs.ansible.com/ansible/2.9/modules/template_module.html#template-module)
- [systemd](https://docs.ansible.com/ansible/2.9/modules/systemd_module.html#systemd-module)
- [command](https://docs.ansible.com/ansible/2.9/modules/command_module.html#command-module)
- [debug](https://docs.ansible.com/ansible/2.9/modules/debug_module.html#debug-module)

> The reason to use the `command` module instead of the `service`, or underline module, has to do on how `auditd` handles stop requests and an issue with ansible and legacy services.

## Role Variables

A few variables are in place at [defaults](./defaults/main.yml) to populate the [setup file](./templates/auditd.conf.j2) template:

- `auditd_max_log_file`: maximum file size in megabytes, default `8`
- `auditd_space_left_action`: tells the system what action to take when the system has detected that it is starting to get low on disk space, default `SYSLOG`
- `audit_action_mail_acct`: should contain a valid email address or alias, default `root`
- `audit_admin_space_left_action`: tells the system what action to take when the system has detected that it is low on disk space, default `halt`
- `audit_max_log_file_action`: tells  the  system what action to take when the system has detected that the max file size limit has been reached, default `keep_log`

> for more information please read the `man auditd.conf`.

## Dependencies

This role doesn't have any dependencies.

## Example Playbook

A working example using Vagrant and Virtual Box is setup under [tests](./tests/).
