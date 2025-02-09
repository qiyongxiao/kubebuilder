[![Build Status](https://travis-ci.org/kubernetes-sigs/kubebuilder.svg?branch=master)](https://travis-ci.org/kubernetes-sigs/kubebuilder "Travis")
[![Go Report Card](https://goreportcard.com/badge/sigs.k8s.io/kubebuilder)](https://goreportcard.com/report/sigs.k8s.io/kubebuilder)

## Kubebuilder

Kubebuilder is a framework for building Kubernetes APIs using [custom resource definitions (CRDs)](https://kubernetes.io/docs/tasks/access-kubernetes-api/extend-api-custom-resource-definitions).

**Note:** kubebuilder does not exist as an example to *copy-paste*, but instead provides powerful libraries and tools
to simplify building and publishing Kubernetes APIs from scratch.

### Builde from source for each platforms

```
miyamoto@macbookpro:>> git clone -b v2.0.0 https://github.com/qiyongxiao/kubebuilder.git $GOPATH/sigs.k8s.io/kubebuilder
miyamoto@macbookpro:>> cd $GOPATH/sigs.k8s.io/kubebuilder
miyamoto@macbookpro:>> vim cmd/version/version.go
var (
    kubeBuilderVersion      = "v2.0.0"
    kubernetesVendorVersion = "v1.13.7"
    goos                    = "linux"
    goarch                  = "mips64le"
    gitCommit               = "b31cc5d96dbc91749eb49c2cf600bd951a46d4bd" // sha1 from git, output of $(git rev-parse HEAD)
    buildDate = "2019-08-31T7:50:00Z"
)
:x
miyamoto@macbookpro:/Users/miyamoto/go/src/sigs.k8s.io/kubebuilder>>make build
go build -o bin/kubebuilder ./cmd
miyamoto@macbookpro:/Users/miyamoto/go/src/sigs.k8s.io/kubebuilder>>./bin/kubebuilder version
Version: version.Version{KubeBuilderVersion:"v2.0.0", KubernetesVendor:"v1.13.7", GitCommit:"b31cc5d96dbc91749eb49c2cf600bd951a46d4bd", BuildDate:"2019-08-31T7:50:00Z", GoOs:"linux", GoArch:"mips64le"}
```

### Installation

It is strongly recommended that you use a released version. Release binaries are available on the [releases](https://github.com/kubernetes-sigs/kubebuilder/releases) page.
Follow the [instructions](https://book.kubebuilder.io/quick-start.html#installation) to install Kubebuilder.


## Getting Started

See the [Getting Started](https://book.kubebuilder.io/quick-start.html) documentation.

![Quick Start](docs/gif/quickstart-1.0.0.gif)

## Documentation

Check out the Kubebuilder [book](https://book.kubebuilder.io).

## Resources

- GitBook: [book.kubebuilder.com](https://book.kubebuilder.io)
- GitHub Repo: [kubernetes-sigs/kubebuilder](https://github.com/kubernetes-sigs/kubebuilder)
- Slack channel: [#kubebuilder](https://slack.k8s.io/#kubebuilder)
- Google Group: [kubebuilder@googlegroups.com](https://groups.google.com/forum/#!forum/kubebuilder)
- Planned Work: [Sprint Dashboard](https://github.com/kubernetes-sigs/kubebuilder/projects/1)
- Design Documents: [designs](designs/).

## Motivation

Building Kubernetes tools and APIs involves making a lot of decisions and writing a lot of boilerplate.

In order to facilitate easily building Kubernetes APIs and tools using the canonical approach, this framework
provides a collection of Kubernetes development tools to minimize toil.

Kubebuilder attempts to facilitate the following developer workflow for building APIs

1. Create a new project directory
2. Create one or more resource APIs as CRDs and then add fields to the resources
3. Implement reconcile loops in controllers and watch additional resources
4. Test by running against a cluster (self-installs CRDs and starts controllers automatically)
5. Update bootstrapped integration tests to test new fields and business logic
6. Build and publish a container from the provided Dockerfile

## Scope

Building APIs using CRDs, Controllers and Admission Webhooks.

## Philosophy

See [DESIGN.md](DESIGN.md) for the guiding principals of the various KubeBuilder projects.

TL;DR:

Provide clean library abstractions with clear and well exampled godocs.

- Prefer using go *interfaces* and *libraries* over relying on *code generation*
- Prefer using *code generation* over *1 time init* of stubs
- Prefer *1 time init* of stubs over forked and modified boilerplate
- Never fork and modify boilerplate

## Techniques

- Provide higher level libraries on top of low level client libraries
  - Protect developers from breaking changes in low level libraries
  - Start minimal and provide progressive discovery of functionality
  - Provide sane defaults and allow users to override when they exist
- Provide code generators to maintain common boilerplate that can't be addressed by interfaces
  - Driven off of `//+` comments
- Provide bootstrapping commands to initialize new packages

## Troubleshooting

- ### Bugs and Feature Requests:
  If you have what looks like a bug, or you would like to make a feature request, please use the [Github issue tracking system.](https://github.com/kubernetes-sigs/kubebuilder/issues)
Before you file an issue, please search existing issues to see if your issue is already covered.

- ### Slack
  For realtime discussion,  you can join the [#kubebuilder](https://slack.k8s.io/#kubebuilder) slack channel. Slack requires registration, but the Kubernetes team is open invitation to anyone to register here. Feel free to come and ask any questions.

## Contributing
Contributions are greatly appreciated. The maintainers actively manage the issues list, and try to highlight issues suitable for newcomers.
The project follows the typical GitHub pull request model. See [CONTRIBUTING.md](CONTRIBUTING.md) for more details.
Before starting any work, please either comment on an existing issue, or file a new one.
