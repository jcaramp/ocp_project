ocp_project
=========

This role implements tasks for manage projects in Openshift.

The role **creates** or **deletes** a project in Openshift.

When **creates** a project, it will be configured with an annotation type ``openshift.io/node-selector``, and sets the value defined in ``project_annotation`` variable. 

Requirements
------------

The below requirements are needed on the host that executes this role.

Minimum Ansible version: 2.8.0

Ansible modules:

- k8s
- k8s_auth
- k8s_info / k8s_facts

Python modules:

- python >= 2.7
- openshift >= 0.6
- PyYAML >= 3.11
- urllib3
- requests
- requests-oauthlib

Role Variables
--------------

Roles needed to use this role:

Variable | Description | Required | Choices/***Defaults***
------------ | ------------- | ------------- | -------------
api_url | Openshift API URL | yes | -
ocp_username |  Openshift Username | no | -
ocp_password | Openshift Password | no | -
ocp_token | Openshift Service Account Access Token | no | -
ocp_verify_ssl | Verify SSL | no | ***true***, false
project_name | Openshift Project Name | yes | -
project_annotation | Defines the valu to set in ``openshift.io/node-selector`` annotation | yes | -
project_action | The action to perform with project | yes | create, delete

Dependencies
------------

No dependencies.

Example Playbook
----------------

This is an example using an API token to authenticate and **create** a project:

    - hosts: servers
      roles:
        - role: ocp_project
          vars:
            api_url: "https://openshift.example.com:6443"
            ocp_token: "{{ service_account_token }}"
            ocp_verify_ssl: false
            project_name: "example-project"
            project_annotation: "env=test"
            project_action: 'create'

And this is an example using an user/password to authenticate and **delete** a project:

    - hosts: servers
      roles:
        - role: ocp_project
          vars:
            api_url: "https://openshift.example.com:6443"
            ocp_username: "clusteradmin"
            ocp_password: "xxxxxxxxxxx"
            ocp_verify_ssl: true
            project_name: "example-project"
            project_action: 'delete'

Platforms
------------

Tested on:

- Red Hat Enterprise Linux 7.7
- Red Hat Openshift Container Platform 4.2

License
-------

GNU General Public License v3.0

Author Information
------------------

This role was written in 2020 by Jesús Carmona Ampuero