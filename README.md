# How to Use

This stack shows you how to setup a split install with an external postgresql node that is installed with PE and an additional PuppetDB node.  

# Things to know

1.  The console node uses a different pe.conf than the rest of the nodes so that it can install PostgreSQL locally and have console-services use the local PostgreSQL.  PuppetDB uses the PostgreSQL install on pe-postgres-node.  

2.  You cannot set `puppet_enterprise::puppetdb_host` to an array so we only set `puppet_enterprise::profile::database::puppetdb_hosts` which allows the second PuppetDB host access to the PostgreSQL install.
 - This means the additional puppetdbs do not show up in the console status widget and that among other things the CLI tools are not configured with backup PuppetDBs if the first is down.  

# To Do

1.  Add another puppetdb node
2.  Laydown an autosign.conf on the CA master that signs the additional puppetdb nodes
 - This can go away after allowing an array of puppetdb_hosts happens
3.  Use the puppetdb_shared_cert module to setup a cert on the puppetdbs that will not break puppetserver 
 - https://github.com/supercow/pizzaops-puppetdb_shared_cert/
