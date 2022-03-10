This document describes the common issues that customers may encounter when using this CI/CD system, and provide a way on how to solve them.

## Table of Contents
- [Table of Contents](#table-of-contents)
- [Gitlab Runner Installation](#gitlab-runner-installation)
  - [Couldn't resolve TCA/ESXi FQDN](#couldnt-resolve-tcaesxi-fqdn)
    - [Resoultion](#resoultion)
  - [Couldn't pull CICD image](#couldnt-pull-cicd-image)

## Gitlab Runner Installation
For other issues which are not listed here, please follow [Gitlab official document](https://docs.gitlab.com/runner/faq/).

### Couldn't resolve TCA/ESXi FQDN
It maybe happen if your environment use your own DNS. 

#### Resoultion
- For runner installation via Docker, you can add an option `--dns=<dns_server_address>` after `docker run` command when starting a new Gitlab Runner.

  For example, if you have a dns server `10.197.66.65`, you can start the runner like this.
  ```bash
     docker run --dns=10.197.66.65 -d --name gitlab-runner --restart always \
     -v /srv/gitlab-runner/config:/etc/gitlab-runner \
     -v /var/run/docker.sock:/var/run/docker.sock \
     gitlab/gitlab-runner:latest
    ```
- For runner installation via Kubernetes, you can edit the Kubernetes cluster DNS settings. 
  
  For example, if the Kubernetes cluster uses CoreDNS and we want to let it resolve dns suffix `tkg.io` using dns server `10.197.66.65`, you can use `kubectl edit configmap coredns -n kube-system`, and add this option.
  ```yaml
  Corefile: |
    tkg.io:53 {
        errors
        forward . 10.197.66.65
        cache 30
        reload
    }
    ```

### Couldn't pull CICD image
If you encounter this issue, please check your runner can connect with `vmwtec.jfrog.io`.