eNiXHosting.filebeat
=========

An Ansible role to deploy Elastic [Filebeat](https://www.elastic.co/products/beats) log shipper.

Requirements
------------

Supported targets:

- Debian 8 "Jessie"
- Debian 9 "Stretch"
- RedHat EL 7


Role Variables
--------------

- `filebeat_modules` - List of modules templates configuration files to add
- `filebeat_modules_sourcedir` - Modules templates directory. Default: `templates/`
- `filebeat_extra_options` - options to add at the end of configuration file
- `filebeat_logstash_enabled` - Is Logstash output enabled. Default: `true`
- `filebeat_logstash_index` - The index root name to write evetns to. Default: `filebeat`
- `filebeat_logstash_hosts` - The list of downstream Logstash servers. Default: `["localhost:5044"]`
- `filebeat_elasticsearch_enabled` - Is ElasticSearch output enabled. Default: `false`
- `filebeat_elasticsearch_hosts` - The list of downstream ElasticSearch servers. Default: `["localhost:9200"]`
- `filebeat_elasticsearch_protocol` - ElasticSearch connection protocl. Default: "http"
- `filebeat_elasticsearch_user` - If auth enabled, provide username
- `filebeat_elasticsearch_password` - If auth enabled, provide password

**Deprecated**
- `filebeat_prospectors` - List of prospectors to fetch data. Defaults to undef.

Dependencies
------------

Ansible roles, can be pulled by ansible-galaxy or by hand in roles/

- `eNiXHosting.elastic_repo`: https://galaxy.ansible.com/eNiXHosting/elastic_repo/.


Usage
-----

Clone this repo into your roles directory:

    $ git clone https://gitlab.enix.org/ansible/ansible-filebeat.git roles/filebeat

Or use Ansible galaxy requirements.yml

    # eNiXHosting.filebeat galaxy role
    - src: eNiXHosting.filebeat

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - role: eNiXHosting.filebeat
           elastic_repo__branch: 6.x
           filebeat_logstash_enabled: false
           filebeat_elasticsearch_enabled: true
           filebeat_elasticsearch_hosts: ["192.168.1.1:9200", "192.168.1.2:9200"]
           filebeat_modules: ['system.yml.j2']
           filebeat_modules_sourcedir: "modules/"
           filebeat_extra_options: |
             xpack.monitoring.enabled: true
             logging.level: debug

Or can be configured in inventory files this way using oneliner:
```
[all:vars]
filebeat_logstash_hosts=["toto:5004"]
filebeat_prospectors=[{"input_type": "log","paths": ["/var/log/apache2/*.log"], "document_type": "apache"}, {"input_type": "log","paths": ["/var/log/syslog","/var/log/messages","/var/log/*.log"],"document_type": "syslog"}]
```

TODO
-----

List of stuff to improve in this role
- readd tls stuff when needed
- A more complete version but without template of configuration is available here https://github.com/DavidWittman/ansible-filebeat.
- Rename vars to filebeat__

License
-------

GPLv2

Author Information
------------------

Laurent CORBES, Based on Artur Melo work at https://github.com/Restless-ET/ansible-role-filebeat
