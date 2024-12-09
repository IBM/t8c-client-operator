Turbonomic Secure Connect K8S Operator
====================

The Turbonomic Secure Connect Kubernetes Operator (aka t8c-client-operator) is a k8s operator that is used to simplify
the deployment of the Turbonomic Secure Connect platform over a k8s cluster.

The t8c-client-operator consists of:
* a docker image (that includes the operator software itself)
* a CRD file that defines the k8s CustomResourceDefinition object (aka the api definition) of
  kind "tc"
* a CR file that creates an instance of "tc", with a specific configuration

We ship a default config/CR file, but ultimately every customer will have its own modified CR
file that they will adapt to their environment and deployment solution.

Operator Backward Compatibility
-------------------------------
The customer CR file is not under our direct control.
**We need to maintain backward compatiblity on it, as much as possible.**

Those are the guidelines that we need to follow when changing its code:
* We cannot release a different operator binary under the same version. If the binary is
  different, then we need to upgrade the version.
  * This means that any changes to the operator files need to be released under a new docker
    image version.
* Backward-compatibility NON-breaking changes:
  * Increase the minor version
  * Document the change made in the [CHANGELOG](CHANGELOG.md) file
* Backward-compatibility breaking changes:
    * Increase the major version
    * Document the change made in the [CHANGELOG](CHANGELOG.md) file and write instructions for the customer on 
      how to migrate its CR file to the new version.

