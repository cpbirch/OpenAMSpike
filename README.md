OpenAMSpike
===========

Configuration and Code to get an OpenAM instance setup to protect resources

"vagrant up" will configure a server to have Apache2 httpd installed and Tomcat7 with OpenAM setup and running.  Tomcat is listening on port 8080 with httpd on port 80.

OpenAM uses cookies for auth tokens so it needs hostnames, these have been defined as:

127.0.0.1	www.openamspike.local
127.0.0.1	openam.openamspike.local

VM has been setup with port forwarding but you'll also need to define the server names in your host OS if you're testing from the host and use the guest VM services.

From the host OS, visit http://openam.openamspike.local:4080/openam/ to get to the OpenAM console.  The website can be visited at http://www.openamspike.local:3080/

To complete the installation and get the authentication working, the web agent must be installed manually.
Visit http://docs.forgerock.org/en/openam/11.0.0/getting-started/index/chap-first-steps.html#install-web-policy-agent and continue from STEP 4 (apache can be stopped with 'sudo service httpd stop').


