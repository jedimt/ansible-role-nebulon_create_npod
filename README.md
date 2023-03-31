Ansible Role: Create Nebulon nPod
=========

Creates a Nebulon nPod cluster. More information on using this role can be found in the
[Nebulon Ansible](https://on.nebulon.com/docs/en-us/tutorials/tutorial-ansible/8041667baadd168c8333f3aa991637c1) tutorial.

Requirements
------------

- Ansible 3.0 (Ansible Core 2.10) or later
- Nebulon nebulon.nebulon_on Ansible module 1.4.0
- Nebulon smartInfrastructure servers with the Nebulon Services Processing Unit (SPU) installed
- Internet connectivity to Nebulon ON UCAPI GraphQL endpoint
- Nebulon Python SDK (nebpyclient) 2.0.8

Role Variables
--------------

There are Nebulon SPU default variables in the defaults/main.yml file. In addition, the following variables
are used in this role:

    # Vault protected credentials. This assumes an Ansible Vault with the vault_neb_username
    # and vault_neb_password variables are defined and passed to the role.
    neb_username: "{{ vault_neb_username }}"
    neb_password: "{{ vault_neb_password }}"

    # Specify a name for the nPod to be created
    npod_name: "Default nPod"

    # Specify the nebulon ON template to use for creating the nPod
    npod_template: "K8s Local"

    # Specify the nebulon ON nPod group to build the nPod in.
    npod_group: Kubernetes

    # Time zone for nPod
    timezone: "US/Pacific"

    # Note to set for the nPod.
    npod_note: "Created by Ansible playbook"

    # Setting this to "present" creates the nPod.
    npod_state: present

Dependencies
------------

None.

Example Playbook
----------------

    # ===========================================================================
    # Create Nebulon nPod
    # ===========================================================================
    - name: Create Nebulon nPod
    hosts: localhost
    connection: local
    gather_facts: false
    tags: play_create_npod

    vars_files:
        # Ansible vault with all required passwords
        - "../../credentials.yml"

    roles:
        - { role: ansible-role-nebulon-create-npod, npod_name: "K8s_Lenovo" }

License
-------

MIT

Author Information
------------------

Aaron Patten
aaronpatten@gmail.com
