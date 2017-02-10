.. This work is licensed under a Creative Commons Attribution 4.0 International License.
.. http://creativecommons.org/licenses/by/4.0
.. (c) 2017 OPNFV Ulrich Kleber (Huawei)


Creating Scenarios
--------------------

Purpose
^^^^^^^^^^^

A new scenario needs to be created, when a new combination of upstream
components or features shall be supported, that cannot be provided with the
existing scenarios in parallel to their existing features.

Typically new scenarios are created as children of existing scenarios.

* In some cases an upstream implementation can be replaced by a different solution.
  The most obvious example here is the SDN controller. In the first OPNFV release,
  only ODL was supported. Later ONOS and OpenContrail were added, thus creating
  new scenarios.

  In most cases, only one of the SDN controllers is needed, thus OPNFV will support
  the different SDN controllers by different scenarios. This support will be long-
  term, so there will be multiple generic scenarios for these options.

* Another usecase is feature incompatibilities. For instance, OVS and FD.io
  cannot be combined today. Therefore we need different scenarios for them.
  If it is expected that such an incompatibility is not solved for longer time,
  there can be even separate generic scenarios for these options.

The overlap between scenarios should only be allowed where they add components
that cannot be integrated in a single deployment.

If scenario A completely covers scenario B, support of scenario B will be
only provided as long as isolation of development risks is necessary.
However, there might be cases where somebody wants to use scenario B
still as a parent for specific scenarios.

This is especially the case for generic scenarios, since they need more CI and testing
resources. Therefore a gating process will be introduced for generic scenarios.


Creating Generic Scenarios
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Generic scenarios provide stable and mature deployments of an OPNFV release. Therefore
it is important to have generic scenarios in place that provide the main capabilities
needed for NFV environments. On the other hand the number of generic scenarios needs
to be limited because of resources.

* Creation of a new generic scenario needs TSC consensus.
* Typically the generic scenario is created by promoting an existing specific
  scenario. Thus the only the additional information needs to be provided.
* The scenario owner needs to verify that the scenario fulfills the above requirements.
* Since specific scenarios typically are owned by the project who have initiated it,
  and generic scenarios provide a much broader set of features, in many cases a
  change of owner is appropriate. In most cases it will be appropriate to assign
  a testing expert as scenario owner.

Creating Specific Scenarios
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

As already stated, typically specific scenarios are created as children of existing
scenarios. The parent can be a generic or a specific scenario.

Creation of specific scenarios shall be very easy and can be done any time. However,
support might be low priority during a final release preparation, e.g. after a MS6.

* The PTL of the project developing the feature(s) or integrating a component etc can
  request the scenario (tbd from whom: CI or release manager, no need for TSC)
* The PTL shall provide some justification why a new scenario is needed.
  It will be approptiate to discuss that justification in the weekly technical
  discussion meeting.
* The PTL should have prepared that by finding support from one of the installers.
* The PTL should explain from which "parent scenario" (see below) the work will start,
  and what are the planned additions.
* The PTL shall assign a unique name. Naming rules will be set by TSC.
* The PTL shall provide some time schedule plans when the scenario wants to join
  a release, when he expects the scenario merge to other scenarios, and he expects
  the features may be made available in generic scenarios.
  A scenario can join a release at the MS0 after its creation.
  It should join a release latest on the next MS0 6 month after its
  creation (that is it should skip only one release) and merge to its parent
  maximum 2 releases later.
  .. Editors note: "2 releases" is rather strict maybe refine?
* The PTL should explain the infrastructure requirements and clarify that sufficient
  resources are available for the scenario.
* The PTL shall assign a scenario owner.
* The scenario owner shall maintain the scenario descriptor file according to the
  template.
* The scenario owner shall initiate the scenario be integrated in CI or releases.
* When the scenario joins a release this needs to be done in time for the relevant
  milestones.


