# Self-contained Ansible distribution
## Tips
Fork from [https://github.com/ownport/portable-ansible](https://github.com/ownport/portable-ansible), but modified the version and added some pip libs which could meet the requirement for deploying [Kubespray](https://github.com/kubernetes-sigs/kubespray) v2.13.0.   

## Included in modified distribution
ansible upgraded from v2.9.2 to v2.9.6, added jinja2, six, markupsafe, etc...

```
ansible==2.9.6
PyYAML==5.2
paramiko==2.7.1
pyasn1==0.4.8
asn1crypto==1.2.0
bcrypt==3.1.7
cffi==1.13.2
PyNaCl==1.3.0
jinja2==2.11.1
six==1.13.0
markupsafe==1.1.1
cryptography==2.8
netaddr==0.7.19
pbr==5.4.4
hvac==0.10.0
jmespath==0.9.5
ruamel.yaml==0.16.10
```


Ansible package with required python modules. No need to install, just download, unpack and use. The main idea of this package is to run Ansible playbooks on local machine



## Included in the distribution

Version: 0.4.1

| Package  | Version |
| -------- | ------- |
| ansible  | 2.9.2   |
| jinja2   | 2.10.3  |
| PyYAML   | 5.2     |
| paramiko | 2.7.1   |
| six      | 1.13.0  |
| cryptography | 2.8 |
| pyasn1   | 0.4.8   |
| asn1crypto | 1.2.0 |
| bcrypt   | 3.1.7   |
| cffi     | 1.13.2  |
| PyNaCl   | 1.3.0   |
| markupsafe | 1.1.1 |

## How to install and use

You just need to download latest version of portable-ansible tarball (.tar.bz2) from
Releases page https://github.com/ownport/portable-ansible/releases and unpack the files

```sh
$ wget https://github.com/ownport/portable-ansible/releases/download/v0.3.0/portable-ansible-v0.3.0-py2.tar.bz2 -O ansible.tar.bz2
$ tar -xjf ansible.tar.bz2
$ python ansible localhost -m ping
 [WARNING]: provided hosts list is empty, only localhost is available

localhost | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```
If you need to run ansible playbooks, after having extracted the tarball contents:

```sh
$ ln -s ansible ansible-playbook
$ python ansible-playbook playbook.yml
```

In the same fashion, to have all the ansible commands, run:
```
for l in config console doc galaxy inventory playbook pull vault;do
  ln -s ansible ansible-$l
done
```

## Supporting additional python packages

Install python packages into `ansible/extras` directory
```
pip install -t ansible/extras <package>
```
or 
```
pip install -t ansible/extras -r requirements.txt
```

Instead of installing the python packages to `ansible/extras`, you can also install them in user directory to be available for ansible:
```
pip install --user -r requirements.txt
```

## Hints

make aliases to portable ansible directory. In the examples below `portable-ansible` installed in `/opt` directory
```
ln -s /opt/ansible /opt/ansible-playbook
```

## Testing

```sh
python3 /opt/ansible-playbook -i 172.17.0.2,  ~/playbooks/remote-via-ssh-key.yaml
```

```sh
python3 /opt/ansible-playbook -i 172.17.0.2, -c paramiko ~/playbooks/remote-via-username-and-password.yaml  --ask-pass
```

## For developers

to create tarball with required packages just run

For python2
```
$ make tarball-py2
```
For python3
```
$ make tarball-py3
```
For both python versions
```
$ make tarballs
```

## Changelog

All notable changes to this project will be documented in the file CHANGELOG.md


## Links

- [ansible/ansible](https://github.com/ansible/ansible) Ansible is a radically simple IT automation platform that makes your applications and systems easier to deploy. Avoid writing scripts or custom code to deploy and update your applications— automate in a language that approaches plain English, using SSH, with no agents to install on remote systems. http://ansible.com/
- [ansible/ansible-modules-core](https://github.com/ansible/ansible-modules-core) Ansible modules - these modules ship with ansible
- [ansible/ansible-modules-extras](https://github.com/ansible/ansible-modules-extras) Ansible extra modules - these modules ship with ansible
