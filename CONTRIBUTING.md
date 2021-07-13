## Commit Guidelines For Helm Operator

The helm operator is typically built/updated upon one or both the below cases: 

- New release of OpenEBS helm charts in [openebs/stable](https://artifacthub.io/packages/helm/openebs/openebs).
- Updates to operator's functionality, i.e., auxiliary steps performed by the operator pre or post install of helm charts

Please consider the steps below while making the commits in order to achieve the above: 

- On newer OpenEBS releases: 
  - Update the makefile with the appropriate `OPENEBS_RELEASE_VERSION`
  - Bump up the operator image
  - Create a new ClusterServiceVersion manifest under the `olm/OPENEBS_RELEASE_VERSION/` folder with the 
    appropriate modifications to the `version` keys, image of the helm-operator (in `deployments` section),
    the example CR spec under `alm-examples` annotation (important) and any other relevant metadata.
  - Update README.md upon any workflow changes
  
- On updates to operator functionality 
  - Update the makefile with appropriate `IMGTAG`
  - Update the operator manifests in deploy/ folder (if applicable)
  - Update the associated CSV's `maturity level` and/or `clusterPermissions` (if applicable)
