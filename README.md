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
docker run -it test_ee_image:latest ansible-galaxy collection list
```
__output:__
```text
# /usr/share/ansible/collections/ansible_collections
Collection        Version
----------------- -------
ansible.posix     1.4.0  
awx.awx           21.0.0 
community.general 5.0.1  
community.vmware  2.5.0  
```