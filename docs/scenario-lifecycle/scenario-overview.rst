.. This work is licensed under a Creative Commons Attribution 4.0 International License.
.. http://creativecommons.org/licenses/by/4.0
.. (c) 2017 OPNFV Ulrich Kleber (Huawei)


.. Scenario Lifecycle
.. ==========================================

Note: This document is still work in progress.

Overview
-------------

Problem Statement:
^^^^^^^^^^^^^^^^^^^

OPNFV provides the NFV reference platform in different variants, using different
upstream open source projects.
In many cases this includes also different upstream projects providing similar or
overlapping functionality.

OPNFV introduces scenarios to define various combinations of components from upstream
projects or configuration options for these components.

The number of such scenarios has increased over time, so it is necessary to clearly
define how to handle the scenarios.

Introduction:
^^^^^^^^^^^^^^^^^^^
Some OPNFV scenarios have an experimental nature, since they introduce
new technologies that are not yet mature enough to provide a stable release.
Nevertheless there also needs to be a way to provide the user with the
opportunity to try these new features in an OPNFV release context.

Other scenarios are used to provide stable environments for users
that wish to build products or live deployments on them.

OPNFV scenario lifecycle process will support this by defining two types of scenarios:

* **Generic scenarios** cover a stable set of common features provided
  by different components and target long-term usage.
* **Specific scenarios** are needed during development to introduce new upstream
  components or new features.
  They are intended to merge with other specific scenarios
  and bring their features into at least one generic scenario.

OPNFV scenarios are deployed using one of the installer tools.
A scenario can be deployed by multiple installers and the result will look
very similar but different. The capabilities provided by the deployments
should be identical. Results of functional tests should be the same,
independent of the installer that had been used. Performance or other
behavioral aspects could be different.
The scenario lifecycle process will also define how to document which installer
can be used for a scenario and how the CI process can trigger automatic deployment
for a scenario via one of the supported installers.

When a developer decides to define a new scenario, he typically will take one
of the existing scenarios and does some changes, such as:

* add additional components
* change a deploy-time configuration
* use a component in a more experimental version

In this case the already existing scenario is called a "parent" and the new
scenario a "child".

Typically parent scenarios are generic scenarios, but this is not mandated.
In most times the child scenario will develop the new functionality over some
time and then try to merge its configuration back to the parent.
But in other cases, the child will introduce a technology that cannot easily
be combined with the parent.
For this case this document will define how a new generic scenario can be created.

Many OPNFV scenarios can be deployed in a HA (high availability) or non-HA
configuration.
HA configurations deploy some components according to a redundancy model,
as the components support.
In these cases multiple deployment options are defined for the same scenario.

Deployment options will also be used if the same scenario can be deployed
on multiple types of hardware, i.e. Intel and ARM.

Every scenario will be described in a scenario descriptor yaml file.
This file shall contain all the necessary information for different users, such
as the installers (which components to deploy etc.),
the ci process (to find the right resources),
the test projects (to select correct test cases), etc.

In early OPNFV releases, scenarios covered components of the infrastructure,
that is NFVI and VIM.
With the introduction of MANO, an additional dimension for scenarios is needed.
The same MANO components need to be used together with each of the infrastructure
scenarios. Thus MANO scenarios will define the MANO components and a list of
infrastructure scenarios to work with. Please note that MANO scenarios follow
the same lifecycle and rules for generic and specific scenarios like the
infrastructure scenarios.

