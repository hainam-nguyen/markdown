# Rabbitmq provisioning on Debian/Ubuntu

-------------------------------------------------------------------------------------------------------------
### How to use:

1. Add/edit users' info in roles/rabbitmq/list_of_users.yaml

   >  Require variables:

   >- { name: '',
   >    passwd: '',
   >    tags: '',
   >    status: '' }

   >  * name: name of users
   >  * passwd: password
   >  * tags: permission of a user, recommend:
   >        *  administartor tag for a devops user
   >        *  leave empty for a application user
   >  * status:
   >        * present (to create)
   >        * absent (to remove)

2. Run ansible-playbook:
```
ansible-playbook -i hosts rabbitmq.yaml
```

-------------------------------------------------------------------------------------------------------------
# Details

**rabbitmq.yaml**
  > now has more options, can be defined with "task_name":
  >    - install.
  >    - add_users.

**handlers**
  - main.yaml
    > contains restart rabbitmq-server function.

**tasks**
  - main.yaml

  - install_rabbitmq.yaml
    > contains steps for rabbitmq-server installation on a Ubuntu server.

  - add_users_rabbitmq.yaml
    > contains steps for adding new users to rabbitmq-server, user info are kept in var/list_of_users.yaml

**vars**
  - installation_info.yaml
    > include variables for related installation information.

  - list_of_users.yaml
    > contains users information to be added in rabbitmq-server

**templates**
  - erlang
    > configures apt to install erlang-* packages from Bintray and not standard Debian or Ubuntu repository:

  - rabbitmq.conf
    > contains basic configuration of rabbitmq-server (recommened for version later than 3.7.9-1)
    Currently, enable listeners.tcp.default = 5672 and management.listener.port = 15672

  - enabled_plugins
    > contains plugins will be enabled for rabbitmq-server
    Currently, enable [rabbitmq_management]
