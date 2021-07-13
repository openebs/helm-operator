# OpenEBS Helm Operator

## Introduction

- This is  a helm operator for openebs
- The content of values.yaml will be placed as spec items in `OpenEBSInstallTemplate` CR 
- The operator watches all namespaces. There is no need for helm client/tiller to be installed.
  (the helm operator imports code from helm project)
- Changes to spec of the CR will behave similar to values override via helm
- All OpenEBS resources have ownerReference of `OpenEBSInstallTemplate` & are deleted upon removal of CR

Example of OpenEBSInstallTemplate CR can be found [here](deploy/crds/openebs_v1alpha1_openebsinstalltemplate_cr.yaml)

## Limitations 

- Release names are auto-generated based on CR UID. Impact is character-length will exceed limit if CR name
  is longer. 
  - Workaround: Give shorter nams: 
  - ER: https://github.com/operator-framework/operator-sdk/issues/1094

- Release namespace doesn't have a field in the spec. (need more exploration) 
  - Workaround: Create ns "openebs" or any desired before applying the CR

- Uninstall of a failed helm release (say, wrong spec) will be stuck. 
  - Workaround: finalizer has to be removed manually 
  - Snippet: 
  ```
    status:
    conditions:
    - lastTransitionTime: "2019-06-28T02:12:46Z"
      status: "True"
      type: Initialized
    - lastTransitionTime: "2019-06-28T02:12:46Z"
      message: 'failed to get release history: release: "example-openebsinstalltemplate-3c4h3yqweylajqktnjs04e135"
        not found'
      reason: UninstallError
      status: "True"
      type: ReleaseFailed
   ```
- Image Maping

     | helm-operator image  | openebs release image |
     | -------------------- | --------------------- |
     | v0.0.1               | 1.0.0                 |
     | v0.0.2               | 1.1.0                 |
     | v0.0.3               | 1.3.0                 |
     | v0.0.4               | 1.4.0                 |
     | v0.0.5               | 1.5.0                 |
     | v0.0.6               | 2.10.0                |
