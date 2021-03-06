[![Build Status](https://travis-ci.com/konveyor/move2kube.svg?branch=master)](https://travis-ci.com/konveyor/move2kube)
[![Docker Repository on Quay](https://quay.io/repository/konveyor/move2kube/status "Docker Repository on Quay")](https://quay.io/repository/konveyor/move2kube)
[![codecov](https://codecov.io/gh/konveyor/move2kube/branch/master/graph/badge.svg?token=QTPK8KN4J5)](https://codecov.io/gh/konveyor/move2kube)
[![License](https://img.shields.io/:license-apache-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0.html)
[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/konveyor/move2kube/pulls)
[![Go Report Card](https://goreportcard.com/badge/github.com/konveyor/move2kube)](https://goreportcard.com/report/github.com/konveyor/move2kube)
[<img src="https://img.shields.io/badge/slack-konveyor/move2kube-green.svg?logo=slack">](https://kubernetes.slack.com/archives/CR85S82A2)

# Move2Kube

Move2Kube is a command-line tool that accelerates the process of re-platforming to Kubernetes/Openshift. It does so by analysing the environment and source artifacts, and asking guidance from the user when required.

![Overview](./imgs/overview.jpg)

## Install

Command line : `curl -L https://raw.githubusercontent.com/konveyor/move2kube/master/scripts/install.sh | bash -`  
UI : Clone `https://github.com/konveyor/move2kube-ui` and run `docker-compose up`. The UI will now be accessible in `http://localhost:8080`.

## Usage

### Simple Usage

`move2kube translate -s src` , where src is the folder containing the source artifacts.

### Involved Usage

![Usage](./imgs/usage.png)

Usage instructions can be found [here](./USAGE.md)  
Some demo usage flows can be found in [here](https://github.com/konveyor/move2kube-demos)

## Prerequisites

* Docker [(MAC](https://docs.docker.com/desktop/)[/Ubuntu](https://docs.docker.com/engine/install/ubuntu/)[/Windows WSL)](https://docs.docker.com/docker-for-windows/wsl/) - If Cloud Native Buildpack (CNB) support is required.

## Development environment setup

1. Obtain a recent version of `golang`. Known to work with `1.15`.
1. Ensure `$GOPATH` is set. If it's not set:
   1. `mkdir ~/go`
   1. `export GOPATH=~/go`
1. Obtain this repo:
   1. `mkdir -p $GOPATH/src/`
   1. Clone this repo into the above directory.
   1. `cd $GOPATH/src/move2kube`
1. Build: `make build`
1. Run unit tests: `make test`

## Artifacts Required

| Source | Artifact available | Features supported |
|:-------|:-------------------|:-------------------|
| Cloud Foundry | Manifest files | Containerization options from buildpacks, Deployment artifacts |
| Cloud Foundry | Manifest files, Source code | Containerization options based on buildpack/source code, Deployment artifacts |
| Cloud Foundry | Manifest files, Source code, Access to running instance | Containerization options based on buildpack/source code, Deployment artifacts, Metadata from runtime |
| Cloud Foundry | Access to running instance |  Metadata from runtime, Containerization options based on buildpack, Deployment artifacts |
| Docker Compose/Swarm | Docker compose files | Deployment artifacts |
| Docker Compose/Swarm | Docker compose files, Docker images | Deployment artifacts, Ability to enhance images to run in secure environments like Openshift. |
| Source Directories | Source code with no source metadata |  Containerization options based on source code, Deployment artifacts |
| Any source | Access to target cluster | Ability to create artifacts customized for that particular cluster with the most preferred GroupVersion for the kind. |

## Output

* Containerization scripts
  * Dockerfile
  * Source 2 Image (S2I)
  * Cloud Native Buildpack
* Deployment artifacts
  * Kubernetes/Openshift Yamls
  * Helm charts
  * Operator
  * Docker compose

## Discussion

* Check out the [document guides](./docs) to extend Move2Kube.
* To discuss with the maintainers, reach out in [slack](https://cloud-native.slack.com/archives/C01AJ5WCXGF) in [cloud-native](https://slack.cncf.io/) workspace.
