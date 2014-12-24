OpenAMSpike
===========

Vagrant and Ansible configuration to get an OpenAM instance setup to protect resources on an apache2 web server.

Setup the VM
------------

`$> vagrant up`

This will configure a server to have Apache2 httpd installed and Tomcat7 with OpenAM setup and running.  Tomcat is listening on port 8080 with httpd on port 80.

OpenAM uses cookies for auth tokens so it needs hostnames, these have been added to the guest VM, defined as:

`127.0.0.1	www.openamspike.local openam.openamspike.local`

You'll need to add this entry to your /etc/hosts file on your host OS.

The VM has been setup with port forwarding.
* 3080 -> 80
* 4080 -> 8080

Once host names are configurated, from the host OS, visit http://openam.openamspike.local:4080/openam/ to get to the OpenAM console.  The website can be visited at http://www.openamspike.local:3080/

Setup OpenAM
------------

Browse to http://docs.forgerock.org/en/openam/11.0.0/getting-started/index/chap-first-steps.html#install-openam

You'll need to complete the configuration for sections 1.4, 1.5 and 1.6.  DO NOT complete 1.7 as this playbook has done most of it.

Steps 1 and 2 have already been completed by this Ansible playbook, please continue from point 3.  Open http://openam.openamspike.local:4080/openam/ in a new window.

Complete the Installation
-------------------------

The web agent must be installed manually, use the following bullet points to answer the wizard questions when runing the three steps below.

* Apache Server Config Directory : /etc/httpd/conf
* OpenAM server URL : http://openam.openamspike.local:8080/openam
* Agent URL : http://www.openamspike.local
* Agent Profile name : WebAgent
* Agent Profile Password file name : /tmp/pwd.txt

1. Login to the VM $> `vagrant ssh`
2. Run the install wizard $> `sudo /opt/web_agents/apache22_agent/bin/agentadmin --install`
3. Start apache $> `sudo service httpd start`

Try it Out
----------

1. If you haven't already done so, ensure you've logged out of the OpenAM console.
2. Browse to http://www.openamspike.local
3. Login as the built-in default OpenAM identity, user `demo` and password `changeit`
4. After successfully logging in, you should be redirected to the default centos web page.

In the web browser, check for the presence of a cookie called `iPlanetDirectoryPro`, this is the session token set by OpenAM which is an encrypted reference to the session that OpenAM maintains for single sign-on.

