enix/ansible-filebeat
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

No dependecies. :-)

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: Restless-ET.filebeat,
             filebeat_prospectors:
               - {
                 document_type: syslog,
                 paths: ['/var/log/syslog']
               }
           }

TODO
-----

List of stuff to improve in this role
- make role fully working on RedHat systems (especially GPG key and repo changes)
- make filebeat_version working again on debian with repo
- check that filebeat service really enabled on system (not the case with basic installation) and so will start on boot
- readd tls stuff when needed

License
-------

MIT

Author Information
------------------

Laurent CORBES, Based on Artur Melo work at https://github.com/Restless-ET/ansible-role-filebeat
