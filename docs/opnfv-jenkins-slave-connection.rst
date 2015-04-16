Jenkins
--------

Jenkins is an extensible open source continuous integration server. See the details from `here <http://jenkins-ci.org/>`_.

Linux Foundation provides Jenkins for OPNFV. You can access it from `this link <https://build.opnfv.org/ci/>`_.

How to Connect Servers from Labs to OPNFV Jenkins
--------------------------------------------------

The method that is normally used for connecting servers(slaves) to Jenkins requires SSH access to servers from outside. This may not be something to fix quickly for all the labs so we use the alternative way to connect slaves to Jenkins.

This alternative uses JNLP. Via JNLP, slaves open connection towards Jenkins instead of Jenkins accessing to them.

The server you want to connect to OPNFV Jenkins must have access to internet obviously.

Please follow below steps to enable this.

* Please create a ticket by sending mail to OPNFV LF Helpdesk first, opnfv-helpdesk@rt.linuxfoundation.org.
* Ensure DNS is setup for your public IP addresses: DNS A records and PTR records need to be matching
* Create a local user on server you want to connect to OPNFV Jenkins. (user could be named jenkins for example)
* Download jenkins war using this link: `http://mirrors.jenkins-ci.org/war/1.599/jenkins.war <http://mirrors.jenkins-ci.org/war/1.599/jenkins.war>`_
* Extract contents, find the file named slave.jar and copy it to somewhere which jenkins user created in first step can access.
* Create a directory /home/jenkins/opnfv_slave_root
* Ping/contact LF(Aric) via chat as getting the server connected requires Aric's help.
* Ask Aric to create a slave on OPNFV Jenkins. The slave should use JNLP as method. (You can mention Ericsson slave so he can copy that slave and do small modifications on it.)
* Provide needed information to Aric such as the IP of the server, name for your slave, slave root ( /home/jenkins/opnfv_slave_root for example) and so on.
* Aric should provide you the key/token you need to use.
* Have a quick try to see if you can establish connection towards OPNFV Jenkins by using below command.
* java -jar slave.jar -jnlpUrl `https://build.opnfv.org/ci/computer/ <https://build.opnfv.org/ci/computer/>`_ <slave_name>/slave-agent.jnlp -secret <token_you_get_from_Aric>
* Navigate to OPNFV Jenkins and look for your slave. It should have some executors in “Idle” state if the connection is successful. (`https://build.opnfv.org/ci/ <https://build.opnfv.org/ci/>`_)
* Aric will probably create a “HelloWorld” job and execute it on the slave to verify basic functionality.
* Once you reach this step, you have the server connection to OPNFV Jenkins completed. You can script the command you used above so the connection between slave and Jenkins can be kept open.

Jenkins Slaves
---------------

The slaves connected to OPNFV Jenkins using the method explained above are listed below.

`https://build.opnfv.org/ci/computer/ <https://build.opnfv.org/ci/computer/>`_

The ones that don't have red cross next to computer icon are fully functional.

Basic Jenkins Setup
--------------------

Certain things need to be set up in order to use Jenkins in CI. Below list contains some of the obvious ones.

------------------------------------------------------
Creating Service/Functional Account and Setting it up
------------------------------------------------------

This is used for connecting slaves to Jenkins. Whatever account is used for connecting slave(s) then used for executing jobs/build.

This account can also be used for running verification jobs on Git commits and giving +1/-1 if certain commit fails passing certain checks such as commit message format, PEP8, and so on. (Account name could be octopus.)

----------------------------------------
Setting up Credentials/Creating Domains
----------------------------------------

This defines who can do what and which credential is valid for which domain and so on.

--------------
Adding Slaves
--------------

These are the servers where the jobs/builds are executed.

--------------
Creating Jobs
--------------

These are the jobs that build software, test it and so on. See notes on Creating/Configuring/Verifying Jenkins Jobs

-------------------
Installing Plugins
-------------------

With plugins new functionality can be added to Jenkins in order to handle SCM stuff, create pipelines, throttle builds, logging/graphing, and so on.

Plugins
--------

Jenkins has hundreds of different plugins that can be installed in order to extend its functionality. One thing to keep in mind is installing huge number of plugins increases the load on the Jenkins master.

Full list of plugins can be seen from `https://wiki.jenkins-ci.org/display/JENKINS/Plugins <https://wiki.jenkins-ci.org/display/JENKINS/Plugins>`_.

---------------
Slave Handling
---------------

* Connecting slaves to Jenkins with SSH: `SSH Slaves Plugin <https://wiki.jenkins-ci.org/display/JENKINS/SSH+Slaves+plugin>`_

---------------
SCM/Git/Gerrit
---------------

* Use Git as SCM: `Git Plugin <https://wiki.jenkins-ci.org/display/JENKINS/Git+Plugin>`_
* Integrate Gerrit with Jenkins: `Gerrit Plugin <https://wiki.jenkins-ci.org/display/JENKINS/Gerrit+Plugin>`_
* Integrate Gerrit with Jenkins to trigger jobs: `Gerrit Trigger Plugin <https://wiki.jenkins-ci.org/display/JENKINS/Gerrit+Trigger>`_

------------
Jobs/Builds
------------

* Create jobs that can trigger other jobs and take action depending on result: `Parameterized Trigger Plugin <https://wiki.jenkins-ci.org/display/JENKINS/Parameterized+Trigger+Plugin>`_
* Create complex/hierarchical jobs: `Multijob Plugin <https://wiki.jenkins-ci.org/display/JENKINS/Multijob+Plugin>`_
* Create jobs programmatically: `Job DSL Plugin <https://wiki.jenkins-ci.org/display/JENKINS/Job+DSL+Plugin>`_
* Create workflows: `Workflow Plugin <https://github.com/jenkinsci/workflow-plugin>`_
* Throttle concurrent builds: `Throttle Concurrent Builds Plugin <https://wiki.jenkins-ci.org/display/JENKINS/Throttle+Concurrent+Builds+Plugin>`_

------------------
Artifact Handling
------------------

* Integrate Jenkins with Artifactory: `Artifactory Plugin <https://wiki.jenkins-ci.org/display/JENKINS/Artifactory+Plugin>`_

---------------------------------
Notification/Email/Visualization
---------------------------------

* Send customized emails: `Email-ext Plugin <https://wiki.jenkins-ci.org/display/JENKINS/Email-ext+plugin>`_
* Make Jenkins talk: `Instant Messaging Plugin <https://wiki.jenkins-ci.org/display/JENKINS/Instant+Messaging+Plugin>`_, `Jabber Plugin <https://wiki.jenkins-ci.org/display/JENKINS/Jabber+Plugin>`_
* Show quick build status: `eXtreme Feedback Plugin <https://wiki.jenkins-ci.org/display/JENKINS/eXtreme+Feedback+Panel+Plugin>`_
* Create and visualize pipelines: `Build Pipeline Plugin <https://wiki.jenkins-ci.org/display/JENKINS/Build+Pipeline+Plugin>`_
* Use Green Balls for successful builds: `Green Balls <https://wiki.jenkins-ci.org/display/JENKINS/Green+Balls>`_

---------------------
Logging and Graphing
---------------------

An easy option to get started with graphing performance and event logs from test runs is to just use Jenkins with some plugins.

The advantage to having Jenkins do this is the data is readily available for each job. As the number of jobs increased and mining, trends, and more sophisticated numerical data analysis and logging investigation is required the data can also be pushed to external databases such as `splunk <https://wiki.opnfv.org/wiki/splunk>`_ and `logstash <https://wiki.opnfv.org/wiki/logstash>`_.

This plugin provides generic plotting (or graphing) capabilities in Jenkins.

This plugin will plot one or more single values variations across builds in one or more plots. Plots for a particular job (or project) are configured in the job configuration screen, where each field has additional help information. Each plot can have one or more lines (called data series). After each build completes the plots' data series latest values are pulled from Java properties file(s), CSV file(s), or XML file(s) via an XPath (which you should have generated during the build) somewhere below you workspace. Data for each plot is stored in a CSV file within the job's root project directory.

It can generate various kind of plots, including Area, Bar, Line, Stacked Bar, Waterfall…

Here is an example of the plots generated by this plugin: 
.. image:: images/exampleplot.png

See more details here: `https://wiki.jenkins-ci.org/display/JENKINS/Plot+Plugin <https://wiki.jenkins-ci.org/display/JENKINS/Plot+Plugin>`_
