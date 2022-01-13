

The OpenSCAP Ansible scripts have been frustrating.

The Ubuntu2004-playbook-stig has incorrect libraries and also removes the NOPASSWD which is fine for deployment but breaks the Vagrant Ubuntu images because the vagrant user uses token authentication and NOPASSWD authentication to run sudo. Use the `ansible.skip_tags = "sudo_require_authentication"` line to skip the authentication changes. However, once past that issue, the playbook quickly runs into incorrect package names and executables.

The Ubuntu2004-playbook-standard does not update partitions.

# Getting Started
## Dependencies

The project has a few dependencies before getting started. VirtualBox will be used for local development to create virtual machines. Vagrant will be used to test the Ansible scripts on virtual machines prior to installing on the physical server. Ansible will be used to automatically configure the server.

| Name | URL |
|---|---|
| HashiCorp Vagrant | https://www.vagrantup.com/downloads |
| HashiCorp Vault | https://www.vaultproject.io/downloads |
| Oracle VirtualBox | https://www.virtualbox.org/wiki/Linux_Downloads |
| RedHat Ansible | https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html |

## Hardening Playbooks

Playbooks to harden the server are downloaded from the ComplianceAsCode github repository.

https://github.com/ComplianceAsCode/content

Unfortunately, there were errors running the Ansible scripts. In order to continue working while waiting for these issues to be corrected, the playbooks have been altered in this project under the `./playbooks/` directory.

## Deployment

This webpage has the vagrant boxes
https://cloud.centos.org/centos/8-stream/x86_64/images/


Add the box locally to Vagrant

```
vagrant box add https://cloud.centos.org/centos/8-stream/x86_64/images/CentOS-Stream-Vagrant-8-20210603.0.x86_64.vagrant-virtualbox.box --name centos/stream8-20210603
```



```
vagrant up
```

If Ansible fails to run,

```
vagrant provision
```




XXX install profiles (these are old)
apt install -t "$(lsb_release -sc) universe" ssg-base ssg-debderived ssg-debian ssg-nondebian ssg-applications



wget https://github.com/ComplianceAsCode/content/releases/download/v0.1.58/scap-security-guide-0.1.58.zip
unzip scap-security-guide-0.1.58.zip 


oscap xccdf eval --profile xccdf_org.ssgproject.content_profile_cis_level1_workstation --results-arf arf.xml --report report.html --oval-results scap-security-guide-0.1.58/ssg-ubuntu2004-ds.xml



oscap xccdf eval --profile xccdf_org.ssgproject.content_profile_cis_level1_server --results-arf arf.xml --report report.html --oval-results /usr/share/xml/scap/ssg/content/ssg-ubuntu2004-ds.xml


