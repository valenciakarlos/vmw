## What's in the Release Notes
The release notes cover the following topics:
- [About Telco CI/CD](#about-telco-ci/cd)
- [Supported Releases](#supported-releases)
- [Known Issues](#known-issues)

## About Telco CI/CD
This is the 1.0.0 version of CI/CD with supports of day 1 operations from ESXi imaging, Zero touch provisioning, Kubernetes cluster creation, CNF onboardings and some kubernetes testings.
Several day 2 operations like CNF reconfiguration and update are also added.


## Supported Releases
### Telco CI/CD 1.0.0
21th January 2021 GA

**New features**
- Support TCA 1.8. TCA 1.8 documentation can be found [here](https://docs.vmware.com/en/VMware-Telco-Cloud-Automation/services/rn/VMware-Telco-Cloud-Automation-Release-Notes.html#new-features-2)
- Separate SDDC setup, Kubernetes cluster management and CNF onboarding into different projects and pipelines.
- Support to handle multiple environment in SDDC project.
- Support to manage multiple K8S cluster templates and clusters in K8S cluster project. 
- Support to enable SR-IOV for ESXi after deploying it.
- Support to onboard External-DNS CNF with TCA 1.8.
- No need to provide placementParams in cluster spec and clusterConfig in cluster template spec if using default values. 


**Downloads**
- CICD Image: vmwtec.jfrog.io/docker-production-cicd/cicd-toolsbox:1.0.0
- Artifacts: 
  - https://vmwtec.jfrog.io/artifactory/generic-cicd-production/1.0.0/hardware-config-1.0.0.zip
  - https://vmwtec.jfrog.io/artifactory/generic-cicd-production/1.0.0/k8s-cluster-1.0.0.zip
  - https://vmwtec.jfrog.io/artifactory/generic-cicd-production/1.0.0/external-dns-1.0.0.zip


## Known Issues
- In case you use TCA 1.7 csar file to update CNF in TCA 1.8 environment, you need to create a new catalog for cnf instance before running cnf update pipeline.  
   There are two possible workarounds:
    - Design a fresh new CSAR from scratch via the UI (drag and drop components).
    - Create a new CSAR outside of TCA by directly unzipping the CSAR, editing the source files and re-zipping it as a new CSAR. Upload csar file to TCA.
