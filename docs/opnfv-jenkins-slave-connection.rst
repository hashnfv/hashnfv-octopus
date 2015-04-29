Jenkins
=======

Jenkins is an extensible open source Continuous Integration (CI) server. [1]

Linux Foundation (LF) hosts and operates `OPNFV Jenkins <https://build.opnfv.org/ci/>`_.

Jenkins Slaves
==============

**Slaves** are computers that are set up to build projects for a **Jenkins Master**. Jenkins runs a separate program called "**slave agent**" on slaves. When slaves are registered to a master, the master starts distributing loads to slaves. Term **Node** is used to refer to all machines that are part of Jenkins grid, slaves and master. [2]

Two types of slaves are currently connected to OPNFV Jenkins and handling different tasks depending on the purpose of connecting the slave.

* Slaves hosted in `LF Lab <https://wiki.opnfv.org/get_started/lflab_hosting#hardware_setup>`_
* Slaves hosted in `Community Test Labs <https://wiki.opnfv.org/pharos#community_test_labs>`_

The slaves connected to OPNFV Jenkins can be seen using this link: https://build.opnfv.org/ci/computer/
The ones that don't have red cross next to computer icon are fully functional.

How to Connect Slaves to OPNFV Jenkins
======================================

The method that is normally used for connecting slaves to Jenkins requires direct SSH access to servers. [3] This is the method that is used for connecting slaves hosted in LF Lab.

Connecting slaves using direct SSH access can become a challenge given that OPNFV Project has number of different labs provided by community as mentioned in previous section. All these labs have different security requirements which can increase the effort and the time needed for connecting slaves to Jenkins. In order to reduce the effort and the time needed for connecting slaves and streamline the process, it has been decided to connect slaves using `Java Network Launch Protocol (JNLP) <https://docs.oracle.com/javase/tutorial/deployment/deploymentInDepth/jnlp.html>`_.

Connecting Slaves from LF Lab to OPNFV Jenkins
----------------------------------------------

Slaves hosted in LF Lab are handled by LF. All the requests and questions regarding these slaves should be submitted to `OPNFV LF Helpdesk <opnfv-helpdesk@rt.linuxfoundation.org>`_.

Connecting Slaves from Community Labs to OPNFV Jenkins
------------------------------------------------------

As noted in corresponding section, slaves from Community Labs are connected using JNLP. Via JNLP, slaves open connection towards Jenkins Master instead of Jenkins Master accessing to them directly.

Servers connecting to OPNFV Jenkins using this method must have access to internet.

Please follow below steps to connect a slave to OPNFV Jenkins.

1. Create a ticket by sending mail to OPNFV LF Helpdesk first, opnfv-helpdesk@rt.linuxfoundation.org.
2. Ensure DNS is setup for your public IP addresses: DNS A records and PTR records need to be matching.
3. Create a local user on server you want to connect to OPNFV Jenkins. (named **jenkins** for example)
4. Download slave.jar using https://build.opnfv.org/ci/jnlpJars/slave.jar and place it to somewhere so jenkins user created in previous step can access.
5. Create a directory /home/jenkins/opnfv_slave_root.
6. Ping/contact LF(Aric) via chat as getting the server connected requires Aric's help.
7. Ask Aric to create a slave on OPNFV Jenkins. The slave should use JNLP as method.
8. Provide needed information to Aric such as the IP of the server, name of the slave, and slave root. (/home/jenkins/opnfv_slave_root for example)
9. Aric should provide you the key/token you need to use.
10. Try to see if you can establish connection towards OPNFV Jenkins by using below command.

``java -jar slave.jar -jnlpUrl https://build.opnfv.org/ci/computer/<slave_name>/slave-agent.jnlp -secret <token>``

11. Navigate to OPNFV Jenkins and look for your slave. It should have some executors in “Idle” state if the connection is successful.
12. Once you reach this step, you have the server connection to OPNFV Jenkins completed. You can script the command you used above so the connection between slave and Jenkins can be kept open.

References
==========
* `What is Jenkins <https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins>`_
* `Jenkins Terminology <https://wiki.jenkins-ci.org/display/JENKINS/Terminology>`_
* `Jenkins SSH Slaves Plugin <https://wiki.jenkins-ci.org/display/JENKINS/SSH+Slaves+plugin>`_

**Documentation tracking**

Revision: _sha1_

Build date:  _date_
