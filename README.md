# Ansible Builder

```shell
ansible-builder build --tag test_ee_image --container-runtime docker -v 3
```
__output:__
```text
.
.
.
Use 'docker scan' to run Snyk tests against images to find vulnerabilities and learn how to fix them

Complete! The build context can be found at: /Users/***/workspace/pycharm/ansible-builder/context
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

ansible-runner run --process-isolation . -p asd.yml --container-volume-mount .:/runner/project --container-image vmware-ee-image:latest

ansible-runner run --process-isolation . --container-volume-mount .:/runner/project --container-image vmware-ee-image:latest -p test.yml --cmdline "--extra-vars 'drmon_api=http://185.81.165.121:9989'"
```




