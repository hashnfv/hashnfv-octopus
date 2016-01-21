===========================
 OPNFV Artifact Repository
===========================

Artifact Repository
===================

What is Artifact Repository
---------------------------

An Artifact Repository is akin to what Subversion is to source code, i.e.
it is a way of versioning artifacts produced by build systems, CI, and so on. [1]

Why Artifact Repository is Needed
---------------------------------

Since many developers check their source code into the GIT repository it may seem natural
to just place the files you've built into the repo too.
This can work okay for a single developer working on a project over the weekends
but with a team working on many components that need to be tested and integrated, this won't scale.

The way git works, no revision of any file is ever lost.
So if you ever check in a big file, the repository will always contain it,
and a git clone will be that much slower for every clone from that point onward.

The golden rule of revision control systems applies:
*check in your build scripts, not your build products*.

Unfortunately, it only takes one person to start doing this and we end up with huge repositories.
Please don't do this. It will make your computers sad.
Thankfully, Gerrit and code review systems are a massive disincentive to doing this.

You definitely need to avoid storing binary images in git. This is what artifact repositories are for. [2]

A “centralized image repository” is needed that can store multiple versions of various virtual machines
and have something like /latest pointing to the newest uploaded image.
It could be a simple nginx server that stores the output images from any jenkins job if it's successful, for instance.

OPNFV Artifact Repository
=========================

What is used as Artifact Repository for OPNFV
---------------------------------------------

Setting up, hosting, and operating an artifact repository on OPNFV Infrastructure
in Linux Foundation (LF) environment requires too much storage space.
It is also not a straightforward undertaking to have robust Artifact Repository and provide 24/7 support.

OPNFV Project decided to use **Google Cloud Storage** as OPNFV Artifact Repository due to reasons summarized above. [3]

Usage of Artifact Repository in OPNFV CI
----------------------------------------

Binaries/packages that are produced by OPNFV Continuous Integration (CI) are deployed/uploaded
to Artifact Repository making it possible to reuse artifacts during later stages of OPNFV CI.
Stored artifacts can be consumed by individual developers/organizations as well.

In OPNFV, we generally produce PDF, ISO and store them on OPNFV Artifact Repository.

OPNFV Artifact Repository Web Interface
----------------------------------------

OPNFV Artifact Repository is accessible via link http://artifacts.opnfv.org/.

A proxy has been set up by LF for the community members located in countries with access restrictions to Google http://build.opnfv.org/artifacts/.

Access Rights to OPNFV Artifact Repository
==========================================

As summarized in previous sections, OPNFV uses Google Cloud Storage as Artifact Repository.
By default, everyone has read access to it and artifacts can be fetched/downloaded using browser,
a curl-like command line HTTP client, or gsutil.

Write access to Artifact Repository is given per request basis and all the requests
must go through `LF Helpdesk <opnfv-helpdesk@rt.linuxfoundation.org>`_ with an explanation
regarding the purpose of write access.
Once you are given write access, you can read corresponding section to store artifacts on OPNFV Artifact Repository.

How to Use OPNFV Artifact Repository
====================================

There are 3 basic scenarios to use OPNFV Artifact repository.

* browsing artifacts
* downloading artifacts
* uploading artifacts

Please see corresponding sections regarding how to do these.

How to Browse Artifacts Stored on OPNFV Artifact Repository
-----------------------------------------------------------

You can browse stored artifacts using

* **Web Browser**: By navigating to the address `OPNFV Artifact Storage <http://artifacts.opnfv.org/>`_.

* **Command Line HTTP-client**
    ``curl -o <output_filename> http://artifacts.opnfv.org``

    Example:

    ``curl -o opnfv-artifact-repo.html http://artifacts.opnfv.org``

* **Google Storage Util (gsutil)**
    ``gsutil ls gs://artifacts.opnfv.org/<path_to_bucket>``

    Example:

    ``gsutil ls gs://artifacts.opnfv.org/octopus``

How to Download Artifacts from OPNFV Artifact Repository
--------------------------------------------------------

You can download stored artifacts using

* **Web Browser**: By navigating to the address `OPNFV Artifact Storage <http://artifacts.opnfv.org/>`_ and clicking the link of the artifact you want to download.

* **Command Line HTTP-client**
    ``curl -o <output_filename> http://artifacts.opnfv.org/<path/to/artifact>``

    Example:

    ``curl -o main.pdf http://artifacts.opnfv.org/octopus/docs/release/main.pdf``

* **Google Storage Util (gsutil)**
    ``gsutil cp gs://artifacts.opnfv.org/<path/to/artifact> <output_filename>``

    Example:

    ``gsutil cp gs://artifacts.opnfv.org/octopus/docs/release/main.pdf main.pdf``

How to Upload Artifacts to OPNFV Artifact Repository
----------------------------------------------------

As explained in previous sections, you need to get write access for OPNFV Artifact Repository
in order to upload artifacts.

Apart from write access, you also need to have Google account and have the
Google Cloud Storage utility, **gsutil**, installed on your computer.

Install and Configure gsutil
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Please follow steps listed below.

1. Install gsutil

    Please follow steps listed on `this link <https://cloud.google.com/storage/docs/gsutil_install>`_ to install gsutil to your computer.

2. Configure gsutil

    Issue below command and follow the instructions. You will be asked for the project-id.
The project-id is **linux-foundation-collab**.

    ``gsutil config``

3. Request write access for OPNFV Artifact Repository

    Send an email to `LF Helpdesk <opnfv-helpdesk@rt.linuxfoundation.org>`_ and list the reasons for the request. Do not forget to include gmail mail address.

Upload Artifacts
~~~~~~~~~~~~~~~~

Once you installed and configured gsutil and got write access from LF Helpdesk,
you should be able to upload artifacts to OPNFV Artifact Repository.

The command to upload artifacts is

    ``gsutil cp <file_to_upload> gs://artifacts.opnfv.org/<path/to/bucket>``

    Example:

    ``gsutil cp README gs://artifacts.opnfv.org/octopus``

Once the upload operation is completed,
you can do the listing and check to see if the artifact is where it is expected to be.

    ``gsutil ls gs://artifacts.opnfv.org/<path/to/bucket>``

    Example:

    ``gsutil ls gs://artifacts.opnfv.org/octopus``

Getting Help
============

Send an email to `LF Helpdesk <opnfv-helpdesk@rt.linuxfoundation.org>`_ or join the channel **#opnfv-octopus** on IRC.

References
----------
1. `Why you should be using an Artifact Repository <http://blogs.collab.net/subversion/why-you-should-be-using-an-artifact-repository-part-1>`_
2. `Regarding VM image and Git repo <http://lists.opnfv.org/pipermail/opnfv-tech-discuss/2015-January/000591.html>`_
3. `Google Cloud Storage <https://cloud.google.com/storage/>`_
