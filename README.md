# Ansible collection: kangaroot.foreman_content_ol

Collection for configuring Oracle Linux repositories and Oracle Linux OS related content in a Foreman/Katello installation.

The Oracle Linux repositories that can be configured from this collection are:

- Oracle Linux 7
- Oracle Linux 8[^1]
- Oracle Linux 9[^1]

The ULN Oracle Linux repositories can be configured instead of the public Oracle Linux repositories. A ULN username and password is required.

[^1]: Enabled by default when enabling Oracle Linux repositories.

## Requirements and Dependencies

Ansible Core 2.13.0 or higher is required for the roles in the collection.

The roles in this collection must be imported by the `kangaroot.foreman` collection. It is possible to directly use the roles in this collection but not recommended.

The `kangaroot.foreman` collection requires the `theforeman.foreman` and `theforeman.operations` collections. To install the required collections, execute:

```shell
ansible-galaxy collection install -r requirements.yml
```

in the collection directory.

## Collection Variables

The group_vars directory contains example vars files for the important variables used in the collection roles.

## Usage

The variable `foreman_content_roles` from the `foreman` role in the `kangaroot.foreman` collection contains a list content roles to import.

Add this collection content role to the `foreman_content_roles` list of content roles to import in your playbook project variables.

For example, add the `foreman_content_roles` variable in your `group_vars/foreman.yml` file of your playbook project:

```yaml
# Foreman content roles to include
foreman_content_roles:
  # Package only content
  - ...

  # OS content
  - kangaroot.foreman_content_ol.foreman_content_ol
  - ...

  # Builtin content
  - kangaroot.foreman_content_builtin.foreman_content_builtin
```

Also ensure that the Oracle Linux repositories are enabled by setting the appropriate enable variables:

```yaml
foreman_enable_ol: true
```

In your playbook, add a task to execute the `kangaroot.foreman.foreman` role:

```yaml
- name: Run kangaroot.foreman roles
  hosts: foreman
  roles:
    - kangaroot.foreman.foreman
```

