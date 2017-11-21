# Vagrant runner

Describe your vagrant box or boxes, by changing a dictionary.
Options
  - hostname - hostname of the machine
  - ram - amount of ram.
  - private network ip - the assigned network ip.
  - cpu count - number of cpu cores.
  - cpu cap - cap the max cpu load.
  - gui - run the box headless or with screen.
  - box - name of the target box.
  - box_version - version of the target box.
  - provision - path to bash script for provisioning.
  - ansible_provision - path to ansible playbook for provisioning.


# Example single box
Example of a single ubuntu box with 256 ram, one cpu core and is provisioned by setup_bash_script.sh.
It is running in headless mode.
``` ruby
nodes = [
    {  
        :hostname => 'mgmt',
        :ram => 256,
        :ip => '10.0.0.10',
        :cpu => 1,
        :cpu_cap => 50,
        :gui => false,
        :box => 'ubuntu/trusty64',
        :provision => 'setup_bash_script.sh',
    }
]
```


# Example multiple boxes
``` ruby
nodes = [
    {  
        :hostname => 'mgmt',
        :ram => 256,
        :ip => '10.0.0.10',
        :cpu => 1,
        :gui => false,
        :box => 'ubuntu/trusty64',
        :provision => 'setup_mgmt_script.sh',
    },
    {  
        :hostname => 'httpd',
        :ram => 512,
        :ip => '10.0.0.20',
        :cpu => 1,
        :gui => false,
        :box => 'ubuntu/trusty64',
        :provision => 'setup_httpd_script.sh',
    },
    {  
        :hostname => 'db',
        :ram => 512,
        :ip => '10.0.0.30',
        :cpu => 1,
        :gui => false,
        :box => 'ubuntu/trusty64',
        :provision => 'setup_db_script.sh',
    }
]
```

