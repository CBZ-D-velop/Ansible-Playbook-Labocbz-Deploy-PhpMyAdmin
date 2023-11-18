# Ansible playbook: labocbz.deploy_phpmyadmin

![Licence Status](https://img.shields.io/badge/licence-MIT-brightgreen)
![CI Status](https://img.shields.io/badge/CI-success-brightgreen)
![Testing Method](https://img.shields.io/badge/Testing%20Method-Ansible%20Molecule-blueviolet)
![Testing Driver](https://img.shields.io/badge/Testing%20Driver-docker-blueviolet)
![Language Status](https://img.shields.io/badge/language-Ansible-red)
![Compagny](https://img.shields.io/badge/Compagny-Labo--CBZ-blue)
![Author](https://img.shields.io/badge/Author-Lord%20Robin%20Crombez-blue)

## Description

![Tag: Ansible](https://img.shields.io/badge/Tech-Ansible-orange)
![Tag: Debian](https://img.shields.io/badge/Tech-Debian-orange)
![Tag: PhpMyAdmin](https://img.shields.io/badge/Tech-PhpMyAdmin-orange)
![Tag: Apache2](https://img.shields.io/badge/Tech-Apache2-orange)
![Tag: SSL/TLS](https://img.shields.io/badge/Tech-SSL%2FTLS-orange)
![Tag: mTLS](https://img.shields.io/badge/Tech-mTLS-orange)
![Tag: MySQL](https://img.shields.io/badge/Tech-MySQL-orange)
![Tag: PHP](https://img.shields.io/badge/Tech-PHP-orange)
![Tag: PHP-FPM](https://img.shields.io/badge/Tech-PHP--FPM-orange)

An Ansible playbook to deploy and configure a PhpMyAdmin instance on your hosts.

This playbook offers a comprehensive solution for deploying a powerful database management tool that streamlines database administration tasks. It manages the installation of the application, facilitating its setup with or without an Apache2 server, ready for enhanced security measures like an application firewall (WAF) and quality of service (QOS) rules. Furthermore, it provides remarkable flexibility by allowing LDAP authentication configuration, mTLS (mutual TLS) implementation, and other advanced security features.

To optimize the application's performance, the playbook also integrates the installation of PHP and PHP FPM. It provides advanced PHP pool management capabilities, allowing the creation and customization of these pools based on specific requirements. Regarding cluster management via Redis, it assumes Redis is already present in the infrastructure, focusing on configuring PhpMyAdmin's integration.

Simplifying the configuration of PhpMyAdmin, the playbook supports a range of YAML objects and specific parameters. It enables the configuration of multiple database servers, simplifying the management of intricate setups.

This playbook extends beyond the installation, handling the creation of specific users tailored for PhpMyAdmin and setting up the necessary databases for its seamless operation.

However, it's important to note that this playbook doesn't cover the installation and creation of a remote administration tool for PhpMyAdmin. It focuses primarily on deploying and configuring the core functionality of the tool itself (accounts, remote access to MySQL/Mariadb).

## Deployment diagramm

![](./assets/Ansible-Playbook-Labocbz-Deploy-PhpMyAdmin.drawio.svg)

Above, we can observe a potential deployment utilizing this playbook. It showcases the PhpMyAdmin system, consisting of multiple components distributed across 3 different hosts. Among these hosts, 2 out of 3 contain Redis and Mariadb services. It's essential to highlight that the playbook requires the presence of an administrative account to create the database and user for PhpMyAdmin. However, the creation of this user and database is managed by the playbook.

We can see the PhpMyAdmin application component, which includes an Apache2 server, the application itself, and a PHP FPM service. Notably, user session data is transmitted to Redis using plaintext and basic authentication due to technical limitations of Redis, a known issue.

Please note that these components can be installed on the same machine. For further details, you can refer to the tests conducted using Molecule. It's evident from these tests that the preparation tasks install and configure Redis and Mariadb on the test host for PhpMyAdmin.

## Tests and simulations

### Basics

You have to run multiples tests. *tests with an # are mandatory*

```MARKDOWN
# lint
# syntax
# converge
# idempotence
# verify
side_effect
```

Executing theses test in this order is called a "scenario" and Molecule can handle them.

Molecule use Ansible and pre configured playbook to create containers, prepare them, converge (run the playbook) and verify its execution.
You can manage multiples scenario with multiples tests in order to get a 100% code coverage.

This playbook contains a ./tests folder. In this folder you can use the inventory or the tower folder to create a simualtion of a real inventory and a real AWX / Tower job execution.

### Command reminder

```SHELL
# Check your YAML syntax
yamllint -c ./.yamllint .

# Check your Ansible syntax and code security
ansible-lint --config=./.ansible-lint .

# Execute and test your playbook
molecule lint
molecule create
molecule list
molecule converge
molecule verify
molecule destroy

# Execute all previous task in one single command
molecule test
```

## Installation

To install this playbook, just copy/import this playbook or raw file into your fresh playbook repository or call it with the "include_playbook/import_playbook" module.

## Usage

### Vars

```YAML
# From inventory
---
# all vars from to put/from your inventory
# see tests/inventory/group_var for all groups and vars.
```

```YAML
# From AWX / Tower
---
tower_env: "local"

```

## Architectural Decisions Records

Here you can put your change to keep a trace of your work and decisions.

### 2023-11-18: First Init

* First init of this playbook with the bootstrap_playbook playbook by Lord Robin Crombez
* Playbook handle the install of Apache2
* Playbook handle the install of PHP
* Playbook handle the install of PHP-FPM
* Playbook handle the install of PhpMyAmdin
* Playbook can create the user and the database for PMA

## Authors

* Lord Robin Crombez

## Sources

* [Ansible playbook documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_playbooks.html)
* [Ansible Molecule documentation](https://molecule.readthedocs.io/)
* [labocbz.prepare_host](https://github.com/CBZ-D-velop/Ansible-Role-Labocbz-Prepare-Host.git)
* [labocbz.add_certificates](https://github.com/CBZ-D-velop/Ansible-Role-Labocbz-Add-Certificates.git)
* [labocbz.install_php](https://github.com/CBZ-D-velop/Ansible-Role-Labocbz-Install-PHP.git)
* [labocbz.add_php_fpm_confs](https://github.com/CBZ-D-velop/Ansible-Role-Labocbz-Add-PHP-FPM-Confs.git)
* [labocbz.add_apache_confs](https://github.com/CBZ-D-velop/Ansible-Role-Labocbz-Add-Apache-Confs.git)
* [labocbz.install_apache](https://github.com/CBZ-D-velop/Ansible-Role-Labocbz-Install-Apache.git)
* [labocbz.install_phpmyadmin](https://github.com/CBZ-D-velop/Ansible-Role-Labocbz-Install-PhpMyAdmin.git)
