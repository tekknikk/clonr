Clonr
==================

Clones of the production postgres database for testing

#Features:
- Instances on Demmad.  Instances are created for each build, then run tests, then terminate.
- Volumes on Demmand.  Volumes are created for pgsql data and log.
- Designed to spin up instances, run tests, then terminate instances.
- Run parallel tests. Support for Multiple builds where each build can have a defined matrix of instance size's and instance counts.
- Newrelic for pgsql metrics

#INSTRUCTIONS:
### 1. Set up your build environment:
- Install AWS CLI
- Configure AWS CLI with a profile
- Install Ansible: http://docs.ansible.com/intro_installation.html
- Set ansible env: shell source ansible env
- Turn host key checking off: shell export ANSIBLE_HOST_KEY_CHECKING=False
- Ansible needs Jinja2: apt-get install python-jinja2
- If old ssh like 5.5: shell export ANSIBLE_SSH_ARGS=""

### 2. Edit build vars in /group_vars/build
- profile: super
- name: victor_frank
- pgsql_data_snap: snap-ce60eff
- pgsql_log_snap: snap-cb0bc0f
- ami_version: 2.4.2
- clones:
-   i2.8xlarge: 8
-   i2.4xlarge: 0
-   i2.2xlarge: 0
- newrelic: 9910108157933df624056a0f5c26f19df6090a28

### 3. Commands
All commands are run from app root.

#### Build
- Command: ansible-playbook -v -i build build.yml
- Output: List of EC2 intance id's and IP addresses || Error

#### Test
- Command: Hey BOB, What command do you run for you test?  I can add it here.
- Output: Success || Error

#### Delete
- Command: ansible-playbook -v -i builds/{{id}}/{{name}}.hosts test.yml
- Output: Success Confirmation || Error

#FAQ
1. How do i run buils in parallel?
Each build needs a unique name

2. I don't want to use Newrelic?
If you don't have a newrelic key or don't want to use newrelic, then comment out the newrelic_key variable in file group_vars/build

#TODO
1. Support Ganglia Monitoring
2. Support Hadoop EMR Builds
3. Needs more tests





