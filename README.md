# VCF Core CLI

[![VCF CLI Core Tests](https://gitlab-vmw.devops.broadcom.net/core-build/workload-cli-core/-/pipelines)](https://gitlab-vmw.devops.broadcom.net/core-build/workload-cli-core/-/pipelines:push+branch:main)
[![VCF CLI Coexistence Tests](https://gitlab-vmw.devops.broadcom.net/core-build/workload-cli-core/-/pipelines)](https://gitlab-vmw.devops.broadcom.net/core-build/workload-cli-core/-/pipelines)

## Overview

The VCF CLI provides integrated and unified command-line access to a broad
array of [products and solutions](https://www.vmware.com/products/cloud-foundation.html) in the
[VMware by Broadcom](https://www.vmware.com/products.html) portfolio.
The CLI is based on a plugin architecture where CLI command functionality can
be delivered through independently developed plugin binaries. To support this
architecture, this project provides releases of the core CLI binary that
plugins integrate with. Said binary serves the role of

1. providing discovery, installation and lifecycle management of plugins on the CLI host
1. providing dispatching of CLI command invocation to a specific plugin
1. providing authentication with and managing access to endpoints which certain CLI commands will target

To facilitate plugin development, the Core CLI also provides

1. the ability to scaffold new plugin projects and plugin commands themselves.
1. the capability to build, test, and publish the plugins being developed.

## Installation

For information on how to install the CLI, see the [Installation Guide](docs/quickstart/install.md)

## Documentation

To get a quick start on how to use VCF CLI, visit the
[Quick Start guide](docs/quickstart/quickstart.md) or visit the
[Full Documentation](docs/full/README.md) for more details.

## Plugin Development

To learn more about how to develop a VCF CLI plugin, see the
[VCF CLI plugin development guide](docs/plugindev/README.md).

### Testing

Plugin developers can use the End-to-End test framework to implement
tests for the functionality of their plugins under a VCF CLI installation.
More details found in the
[End-to-End framework and test case implementation](test/e2e/README.md).
Currently, CLI E2E framework does not support backward compatibility.

## Contributing

Thanks for taking the time to join our community and start contributing! We
welcome pull requests. Feel free to dig through the
[issues](https://gitlab-vmw.devops.broadcom.net/core-build/workload-cli-core/-/issues) and jump in.

### Before you begin

- Check out the [contribution guidelines](CONTRIBUTING.md) to learn more about how to contribute.
- Check out the document [here](docs/community/support.md) about the project's support process.

## Development

Details about how to get started with development for this project can be found
in the [Development Guide](docs/dev/README.md).

## Testing

Unit and Integration tests implementation is part of CLI Core development.
CLI core does have end-to-end test case implementation.
More details found in the [End-to-End framework and test case implementation](test/e2e/README.md).
