
ansible-role-kale
=========

Mounts NFS points and creates AD authentication configuration.
After first  AD authentication createClusterUser script will configure user specific settings.  


Requirements
------------

An NFS server, Login server and Install Server


Role Variables
--------------


all:

<pre>
nfs_mount_point:
  - /data0
  - /data1

nfs_mount: |
  192.168.1.6:/data0   /data0           nfs4 defaults 0 0
  192.168.1.6:/data1   /data1           nfs4 defaults 0 0
</pre>

install:
<pre>
# AD user creation script
user_create_script_enabled: True
user_create_script: "/usr/sbin/createClusterUser"
</pre>

login:

<pre>
# AD authentication
adauth_kale_enabled: "True"
adauth_realm: "ad.example"
ldap_user_search_base: "OU=adUsers,DC=ad,DC=example,DC=com"
ldap_group_search_base: "OU=adGroups,DC=ad,DC=example,DC=com"
ldap_base: "dc=example,dc=com"
ldap_uri: "ldaps://example-ldap-server.com/"
ldap_cacertfile: "/etc/pki/tls/certs/ldapcacert.pem"
pam_use_sssd: True
pamexec_script: "/usr/sbin/pam_aduser"
user_create_script: "/usr/local/sbin/createClusterUser"

# AD host servers
ad_hosts: |
 192.168.1.100	   xxx-ad.example.com ForestDnsZones.ad.example.com
 192.168.1.102     xxx-ad.example.com ForestDnsZones.ad.example.com

</pre>



Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: install, login
      roles:
         - { role: ansible-role-kale }

License
-------

MIT

Author Information
------------------
