Project: Continuous Integration (Octopus)
==========================================

Introduction
-------------

Problem Statement:
^^^^^^^^^^^^^^^^^^^

OPNFV will use many upstream open source projects to create the reference platform.
All these projects are developed and tested independently and in many cases,
not have use cases of other projects in mind.
Therefore it is to be expected that integration of these projects probably will unveil some gaps in functionality,
since testing the OPNFV use cases needs the interworking of many upstream projects.
Thus this integration work will bring major benefit to the community.

Therefore the goal of the CI project – Octopus – is to quickly provide
prototype integration of a first set of upstream projects.
Step by step this later will be evolved to a full blown development environment with
automated test and verification as a continuous integration environment, supporting both,
the parallel evolutionary work in the upstream projects, and the improvement of NFV support in this reference platform.

Summary
^^^^^^^^

The CI project provides the starting point for all OPNFV development activities.
It starts by integrating stable versions of basic upstream projects,
and from there creates a full development environment for OPNFV including automatic builds and basic verification.
This is a very complex task and therefore needs a step by step approach.
At the same time it is urgent to have a basic environment in place very soon.

* **Create a hierarchical build environment** for the same integrated upstream projects as "getstarted",
that uses the build tools as defined by each of the upstream projects and combines them.
This allows development and verification in OPNFV collaborative projects.

* **Implement automatic build process on central servers** - Provide automation and periodic builds

* **Execute the continuous automated builds and basic verification**
