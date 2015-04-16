TL;DR
-----

Don't use git to store binary files that are built from source such as PDF files or Virtual Machine Images.

What is Artifact Repository
---------------------------

An artifact repository is akin to what Subversion is to source code, i.e. it is a way of versioning code binary artifacts. In the Java world these artifacts could be jars, wars, ears, fully fledged applications, libraries or a collections of libraries that are packaged. (Read the rest from `the reference <http://blogs.collab.net/subversion/why-you-should-be-using-an-artifact-repository-part-1>`_.)

What will be used as Artifact Repository for OPNFV
--------------------------------------------------

It has been decided to use Google Storage as OPNFV Artifact Repository.

This is due to not having enough storage in OPNFV infrastructure and installing/managing a robust Artifact Repository is not straightforward.

Alternatives
------------

There are number of different alternatives that can serve as Artifact Repository Manager (ARM).

Well known ones are 

* `JFrog Artifactory <http://www.jfrog.com/open-source/>`_
* `Sonatype Nexus <http://www.sonatype.org/nexus/>`_
* `Apache Archiva <http://archiva.apache.org/index.cgi>`_
* `Swift <https://wiki.openstack.org/wiki/Swift>`_
* `Google Cloud Storage <https://cloud.google.com/storage/>`_

What other OSS Projects Use
---------------------------

Different OSS Projects use different ARMs as listed below.

* OpenDaylight: Sonatype Nexus. (provided by Linux Foundation.) `https://wiki.opendaylight.org/view/Infrastructure:Nexus <https://wiki.opendaylight.org/view/Infrastructure:Nexus>`_.
* OpenStack: Uses tarball site. `http://tarballs.openstack.org/ <http://tarballs.openstack.org/>`_.
* Apache: Sonatype Nexus. `https://repository.apache.org/ <https://repository.apache.org/>`_.

Use of ARM in CI
----------------

Binaries/packages that are produced by CI can be deployed/uploaded to Artifact Repository making it possible to reuse artifacts during later stages of CI. They can be consumed by individual developers/organizations as well.

Whatever is produced by CI can always be tracked by doing this when needed.

Uploading artifacts using REST
------------------------------

Both Artifactory and Nexus provide REST APIs to upload/manipulate artifacts. Below are the links to some examples.

* `How can I programatically upload an artifact into Nexus? <https://support.sonatype.com/entries/22189106-How-can-I-programatically-upload-an-artifact-into-Nexus->`_
* `Deploy Artifact to Artifactory <http://www.jfrog.com/confluence/display/RTF/Artifactory+REST+API#ArtifactoryRESTAPI-DeployArtifact>`_

Uploading artifacts using Jenkins Plugins
-----------------------------------------

Jenkins has number of plugins that offer integration of different ARMs. One of the examples is `Artifactory Plugin <https://wiki.jenkins-ci.org/display/JENKINS/Artifactory+Plugin>`_.

Longer version
--------------

This is a summary of various email discussions on the topic of where to store large binary image files. Typical examples include videos, virtual machine images, software installers, ISOs for Operating Systems.

Since many developers check their source code into the GIT repository it may seem natural to just place the files you've built into the repo too. This can work okay for a single developer working on a project over the weekends but with a team working on many components that need to be tested and integrated this won't scale.

The way git works, no revision of any file is ever lost. So if you ever check in a big file, the repository will always contain it, and a git clone will be that much slower for every clone from that point onward.

The golden rule of revision control systems applies: check in your build scripts, not your build products.

Unfortunately, it only takes one person to start doing this and we end up with huge repositories. Please don't do this. It will make your computers sad. Thankfully, gerrit and code review systems are a massive disincentive to doing this.

You definitely need to avoid storing binary images in git. This is what artifact repositories are for, like `Nexus or Artifactory <https://twiki.auscope.org/wiki/Grid/NexusVsArtifactory>`_

A “centralized image repository” is needed that can store multiple versions of various virtual machines and have something like /latest pointing to the newest uploaded image. It could be a simple nginx server that stores the output images from any jenkins job if it's successful, for instance. Any “client” would be able to fetch the latest “autorelease” using `https://server/image/latest <https://server/image/latest>`_ to get the latest image or `https://server/stcv/1.1 <https://server/stcv/1.1>`_ and so on for any older image.

For the specific project “vswitch performance characterization”, we have a directory as place holder to store the VM images. The VM images are not going to be in git repo. We use the same working git repository inside VM to run initial setup, and save the VM image in the host.

TAG: GIT repository file download section

