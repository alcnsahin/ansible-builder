# Ansible Execution Environment

## Environments
```shell
[ec2-user@ip ~]$ cat /etc/os-release 
NAME="Red Hat Enterprise Linux"
VERSION="8.6 (Ootpa)"
ID="rhel"
ID_LIKE="fedora"
VERSION_ID="8.6"
PLATFORM_ID="platform:el8"
PRETTY_NAME="Red Hat Enterprise Linux 8.6 (Ootpa)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:redhat:enterprise_linux:8::baseos"
HOME_URL="https://www.redhat.com/"
DOCUMENTATION_URL="https://access.redhat.com/documentation/red_hat_enterprise_linux/8/"
BUG_REPORT_URL="https://bugzilla.redhat.com/"

REDHAT_BUGZILLA_PRODUCT="Red Hat Enterprise Linux 8"
REDHAT_BUGZILLA_PRODUCT_VERSION=8.6
REDHAT_SUPPORT_PRODUCT="Red Hat Enterprise Linux"
REDHAT_SUPPORT_PRODUCT_VERSION="8.6"

[ec2-user@ip test]$ pip --version
pip 19.3.1 from /home/ec2-user/test/builder/lib64/python3.8/site-packages/pip (python 3.8)
```

## Installation
```shell
mkdir ~/ansible-builder && cd ~/ansible-builder
python -m venv builder
source builder/bin/activate
pip3.8 install ansible
pip3.8 install ansible-builder
pip3.8 install ansible-runner
```

## Build
```shell
podman build -f context/Containerfile -t vmware-ee-image context
```

## List the collections
```shell
(builder) [root@ip demo]# podman run -it vmware-ee-image:latest ansible-galaxy collection list

# /usr/share/ansible/collections/ansible_collections
Collection              Version
----------------------- -------
amazon.aws              2.0.0  
ansible.controller      4.1.2  
ansible.netcommon       2.4.0  
ansible.network         1.2.0  
ansible.posix           1.2.0  
ansible.security        1.0.0  
ansible.utils           2.4.2  
ansible.windows         1.7.3  
arista.eos              3.1.0  
cisco.asa               2.1.0  
cisco.ios               2.5.0  
cisco.iosxr             2.5.0  
cisco.nxos              2.7.1  
cloud.common            2.0.3  
community.general       5.1.1  
community.vmware        2.6.0  
frr.frr                 1.0.3  
ibm.qradar              1.0.3  
junipernetworks.junos   2.7.1  
kubernetes.core         2.1.1  
openvswitch.openvswitch 2.0.2  
redhat.insights         1.0.5  
redhat.openshift        2.0.1  
redhat.rhv              1.4.4  
redhat.satellite        2.2.0  
servicenow.itsm         1.2.0  
splunk.es               1.0.2  
trendmicro.deepsec      1.1.0  
vmware.vmware_rest      2.1.0  
vyos.vyos               2.6.0  
```

## Test the 'test_ee_image' Image
```shell
ansible-runner run --process-isolation demo -p test.yml --container-image test_ee_image:latest
cd demo/
ansible-runner run --process-isolation . --container-volume-mount .:/runner/project --container-image vmware-ee-image:latest -p test.yml --cmdline "--extra-vars 'drmon_api=http://185.81.165.121:9989'"
```

## Add the image to Ansible Automation Platform

You can try the ee which I have already pushed to quay.io with the following instructions.

```shell
su - awx
podman pull quay.io/alcnsahin/ansible-execution-environment
podman image ls
```
After pulling, open the Automation platform and add a new execution environment with this image.


