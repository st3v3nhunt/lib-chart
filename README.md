# Helm 3 - Library Chart

> Setup a chart to use a library chart based on
[Helm 3 library charts](https://helm.sh/docs/topics/library_charts/)

## Overview

Following the guidance from
[Helm 3 library charts](https://helm.sh/docs/topics/library_charts/)
this repo represents a simple chart, `mychart`, that uses a library chart
`mylibchart` which itself uses the
[common Helm helper chart](https://github.com/helm/charts/tree/master/incubator/common)
as a dependency to acquire some common functions i.e. `common.util.merge`.

### Add incubator chart repo to client

The list of repos added to the local client can be discovered by
`helm repo list`. If it doesn't include `incubator` it will need to be added.

In order to use the external dependency of the common helper chart the
[incubator](https://kubernetes-charts-incubator.storage.googleapis.com/) chart
repository needs to be added to the repos accessible by the client. This is
achieved via
`helm repo add incubator https://kubernetes-charts-incubator.storage.googleapis.com/`

### Update dependencies

As changes are made to the local library chart the consuming chart needs to be
instructed to update to the latest version. This is achieved via
`helm dependency update` (within the root of the chart directory i.e. `mychart`)

### Test chart install

Test the chart installation - `helm install libdemo mychart/ --debug --dry-run`.
The configmap should include the value added in `mychart` (which have
overridden the default, empty values set in `mylibchart`).

The chart can be installed in to a cluster if so wished but it is not necessary
to provide the concept of library charts is working.
