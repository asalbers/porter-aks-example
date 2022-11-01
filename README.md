# Porter AKS cluster deploy

## Running the Bundle

### Setup

Generate credentials or use the existing aks.json file in the repo

```sh
 porter credentials create aks.json
```
Sample output from generate credentials shows sourcing from environment variables.

```sh
porter credentials apply aks.json 
```

```sh
porter credentials show aks-porter

Name: aks-porter
Namespace:
Created: 0001-01-01
Modified: 1 minute ago

-----------------------------------------------------
  Name               Local Source       Source Type
-----------------------------------------------------
  AZURE_CLIENT_ID    AZURE_CLIENT_ID    env
  AZURE_SP_PASSWORD  AZURE_SP_PASSWORD  env
  AZURE_TENANT       AZURE_TENANT       env
  AZURE_TENANT       AZURE_TENANT       env


```

### Install the bundle

The command below installs the porter bundle. Replace the items in <> with your values.

```sh
porter install <name of bundle> -c <credentials name> -r ghcr.io/asalbers/porter-aks-deploy:v0.1.0
```

Sample output

```sh
Building bundle ===>
exit status 1
Copying porter runtime ===>
Copying mixins ===>
Copying mixin exec ===>
Copying mixin az ===>
Building invocation image
[+] Building 196.6s (23/23) FINISHED
 => [internal] load build definition from Dockerfile                                                                                                                   0.0s
 => => transferring dockerfile: 1.23kB                                                                                                                                 0.0s
 => [internal] load .dockerignore                                                                                                                                      0.0s
 => => transferring context: 35B                                                                                                                                       0.0s
 => resolve image config for docker.io/docker/dockerfile-upstream:1.4.0                                                                                              192.1s
 => CACHED docker-image://docker.io/docker/dockerfile-upstream:1.4.0@sha256:178c4e4a93795b9365dbf6cf10da8fcf517fcb4a17f1943a775c0f548e9fc2ff                           0.0s
 => [internal] load .dockerignore                                                                                                                                      0.0s
 => [internal] load build definition from Dockerfile                                                                                                                   0.0s
 => [internal] load metadata for docker.io/library/debian:stretch-slim                                                                                                 0.0s
 => [internal] load build context                                                                                                                                      1.0s
 => => transferring context: 127.38MB                                                                                                                                  1.0s
 => [stage-0  1/14] FROM docker.io/library/debian:stretch-slim                                                                                                         0.0s
 => CACHED [stage-0  2/14] RUN useradd nonroot -m -u 65532 -g 0 -o                                                                                                     0.0s
 => CACHED [stage-0  3/14] RUN rm -f /etc/apt/apt.conf.d/docker-clean; echo 'Binary::apt::APT::Keep-Downloaded-Packages "true";' > /etc/apt/apt.conf.d/keep-cache      0.0s
 => CACHED [stage-0  4/14] RUN --mount=type=cache,target=/var/cache/apt --mount=type=cache,target=/var/lib/apt     apt-get update && apt-get install -y ca-certificat  0.0s
 => CACHED [stage-0  5/14] RUN apt-get update && apt-get install -y apt-transport-https lsb-release gnupg curl                                                         0.0s
 => CACHED [stage-0  6/14] RUN curl -sL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > /etc/apt/trusted.gpg.d/microsoft.asc.gpg                   0.0s
 => CACHED [stage-0  7/14] RUN echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $(lsb_release -cs) main" > /etc/apt/sources.list.d/azure-cli.li  0.0s
 => CACHED [stage-0  8/14] RUN apt-get update && apt-get install -y azure-cli                                                                                          0.0s
 => [stage-0  9/14] COPY --link . /cnab/app                                                                                                                            0.3s
 => [stage-0 10/14] RUN rm /cnab/app/porter.yaml                                                                                                                       0.4s
 => [stage-0 11/14] RUN rm -fr /cnab/app/.cnab                                                                                                                         0.6s
 => [stage-0 12/14] COPY --link .cnab /cnab                                                                                                                            0.2s
 => [stage-0 13/14] RUN chgrp -R 0 /cnab && chmod -R g=u /cnab                                                                                                         0.8s
 => [stage-0 14/14] WORKDIR /cnab/app                                                                                                                                  0.1s
 => exporting to image                                                                                                                                                 0.8s
 => => exporting layers                                                                                                                                                0.7s
 => => writing image sha256:53ceb5018124172b75407e9e499fa837d8e8c229a22e2ed4cbb6c07aef5f9eb9                                                                           0.0s
 => => naming to ghcr.io/asalbers/porter-aks-deploy:porter-d683291e06b57c8fb357046a9fb2dc57                                                                            0.0s
executing install action from porter-aks-deploy (installation: /porter-aks-deploy)
Azure CLI login
Setting the Azure subscription...
Creating resource group...
Creating aks cluster...

World 2.0
Hello World
execution completed successfully!
```

### Uninstalling the Bundle

```sh
porter uninstall <bundle name> -c <credential name> -r ghcr.io/asalbers/porter-aks-deploy:v0.1.0
```

```sh
Building bundle ===>
exit status 1
Copying porter runtime ===>
Copying mixins ===>
Copying mixin exec ===>
Copying mixin az ===>
Building invocation image
[+] Building 62.4s (23/23) FINISHED
 => [internal] load build definition from Dockerfile                                                                                                                   0.0s
 => => transferring dockerfile: 1.23kB                                                                                                                                 0.0s
 => [internal] load .dockerignore                                                                                                                                      0.0s
 => => transferring context: 35B                                                                                                                                       0.0s
 => resolve image config for docker.io/docker/dockerfile-upstream:1.4.0                                                                                               58.0s
 => CACHED docker-image://docker.io/docker/dockerfile-upstream:1.4.0@sha256:178c4e4a93795b9365dbf6cf10da8fcf517fcb4a17f1943a775c0f548e9fc2ff                           0.0s
 => [internal] load .dockerignore                                                                                                                                      0.0s
 => [internal] load build definition from Dockerfile                                                                                                                   0.0s
 => [internal] load metadata for docker.io/library/debian:stretch-slim                                                                                                 0.0s
 => [stage-0  1/14] FROM docker.io/library/debian:stretch-slim                                                                                                         0.0s
 => [internal] load build context                                                                                                                                      1.0s
 => => transferring context: 127.38MB                                                                                                                                  1.0s
 => CACHED [stage-0  2/14] RUN useradd nonroot -m -u 65532 -g 0 -o                                                                                                     0.0s
 => CACHED [stage-0  3/14] RUN rm -f /etc/apt/apt.conf.d/docker-clean; echo 'Binary::apt::APT::Keep-Downloaded-Packages "true";' > /etc/apt/apt.conf.d/keep-cache      0.0s
 => CACHED [stage-0  4/14] RUN --mount=type=cache,target=/var/cache/apt --mount=type=cache,target=/var/lib/apt     apt-get update && apt-get install -y ca-certificat  0.0s
 => CACHED [stage-0  5/14] RUN apt-get update && apt-get install -y apt-transport-https lsb-release gnupg curl                                                         0.0s
 => CACHED [stage-0  6/14] RUN curl -sL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > /etc/apt/trusted.gpg.d/microsoft.asc.gpg                   0.0s
 => CACHED [stage-0  7/14] RUN echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $(lsb_release -cs) main" > /etc/apt/sources.list.d/azure-cli.li  0.0s
 => CACHED [stage-0  8/14] RUN apt-get update && apt-get install -y azure-cli                                                                                          0.0s
 => [stage-0  9/14] COPY --link . /cnab/app                                                                                                                            0.2s
 => [stage-0 10/14] RUN rm /cnab/app/porter.yaml                                                                                                                       0.4s
 => [stage-0 11/14] RUN rm -fr /cnab/app/.cnab                                                                                                                         0.5s
 => [stage-0 12/14] COPY --link .cnab /cnab                                                                                                                            0.3s
 => [stage-0 13/14] RUN chgrp -R 0 /cnab && chmod -R g=u /cnab                                                                                                         0.8s
 => [stage-0 14/14] WORKDIR /cnab/app                                                                                                                                  0.1s
 => exporting to image                                                                                                                                                 0.7s
 => => exporting layers                                                                                                                                                0.7s
 => => writing image sha256:f1fc508e00fbf4cf4cdabe526e6cef6de9a7d22d02f89fa1d5e275ae38bb8f87                                                                           0.0s
 => => naming to ghcr.io/asalbers/porter-aks-deploy:porter-d683291e06b57c8fb357046a9fb2dc57                                                                            0.0s
uninstalling bundle
executing uninstall action from porter-aks-deploy (installation: /porter-aks-deploy)
Azure CLI login
Setting the Azure subscription....
Deleting the cluster...
Deleting resource group...
Uninstall Hello World
Goodbye World
execution completed successfully!
```

# Contents

## porter.yaml

### Parameters

| Name                      | Description                                                                                                    | Type   | Default       | Required | Applies to         |
|---------------------------|----------------------------------------------------------------------------------------------------------------|--------|---------------|----------|--------------------|
| aks_name        | cluster name                                           | string | porter-aks       | false    | All Actions        |
| rg | The azure resource group to use or create for the cluster resources.                                           | string | testrg | false    | ALL Actions        |
| k8s_version             | kubernetes version                                                                             | string  | 1.24.6         | true     | ALL Actions |

### Credentials

| Name                | Description | Required | Applies to |
|---------------------------|----------------------------------------------------------------------------------|----------|-------------|
| AZURE_CLIENT_ID           | The client id for the service principal used to automate the bundle's actions.   | true     | All Actions |
| AZURE_SP_PASSWORD         | The service principal password that is used to log into Azure inside the bundle. | true     | All Actions |
| AZURE_SUB_ID     | The Azure subscription into which to deploy.                                     | true     | All Actions |
| AZURE_TENANT    | The tenant identity in which the service principal resides.                      | true     | All Actions |

## helpers.sh

used for example purposes

## Dockerfile.tmpl

This is a template Dockerfile for the bundle's invocation image. You can
customize it to use different base images, install tools and copy configuration
files. Porter will use it as a template and append lines to it for the mixin and to set
the CMD appropriately for the CNAB specification. You can delete this file if you don't
need it.

Add the following line to **porter.yaml** to enable the Dockerfile template:

```yaml
dockerfile: Dockerfile.tmpl
```

By default, the Dockerfile template is disabled and Porter automatically copies
all of the files in the current directory into the bundle's invocation image. When
you use a custom Dockerfile template, you must manually copy files into the bundle
using COPY statements in the Dockerfile template.

## .gitignore

This is a default file that we provide to help remind you which files are
generated by Porter, and shouldn't be committed to source control. You can
delete it if you don't need it.

## .dockerignore

This is a default file that controls which files are copied into the bundle's
invocation image by default. You can delete it if you don't need it.