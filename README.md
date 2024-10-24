# VCF Core CLI

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