enix/filebeat
=========

An Ansible role for Logstash's Filebeat log shipper.

Requirements
------------

Nothing worth mentioning ...

Role Variables
--------------

- `filebeat_version` - The filebeat version to install. Defaults to: `1.0.1`
- `filebeat_prospectors` - List of prospectors to fetch data.
- `filebeat_logstash_enabled` - If Logstash output if enabled or not. Defaults to: `true`
- `filebeat_logstash_index` - The index root name to write evetns to. Defaults to: `filebeat`
- `filebeat_logstash_hosts` - The list of downstream Logstash servers. Defaults to: `["localhost:5044"]`
- `filebeat_logstash_tls_insecure` - If the client skips verification of server certificates and host names. Defaults to: `false`
- `filebeat_logstash_tls_certificate` - The path to your SSL client certificate.
- `filebeat_logstash_tls_certificate_key` - The path to your SSL client certificate key.
- `filebeat_logstash_tls_certificate_authorities` - The list of paths to root certificates for server verifications.
- `filebeat_logstash_tls_timeout` - Network timeout in seconds. Defaults to: `15`


Dependencies
------------

Ansible roles, can be pulled by ansible-galaxy or by hand in roles/

- `Enix/elastic-repo`: https://gitlab.enix.org/ansible/ansible-elastic-repo.git.


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: filebeat,
             filebeat_prospectors:
               - {
                 document_type: syslog,
                 paths: ['/var/log/syslog']
               }
           }

Or can be configured in inventory files this way using oneliner:
```
[all:vars]
filebeat_logstash_hosts=["toto:5004"]
filebeat_prospectors=[{"input_type": "log","paths": ["/var/log/apache2/*.log"], "document_type": "apache"}, {"input_type": "log","paths": ["/var/log/syslog","/var/log/messages","/var/log/*.log"],"document_type": "syslog"}]
```

TODO
-----

List of stuff to improve in this role
- make role fully working on RedHat systems (especially GPG key and repo changes)
- make filebeat_version working again on debian with repo
- readd tls stuff when needed
- A more complete version but without template of configuration is available here https://github.com/DavidWittman/ansible-filebeat.

License
-------

MIT

Author Information
------------------

Laurent CORBES, Based on Artur Melo work at https://github.com/Restless-ET/ansible-role-filebeat
