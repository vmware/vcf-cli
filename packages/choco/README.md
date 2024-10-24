# Using Chocolatey to install the VCF CLI

This document describes how to build a Chocolatey package for the VCF CLI and
how to install it.

There are two package names that can be built:

1. "vcf-cli" for official releases
2. "vcf-cli-unstable" for pre-releases

The name of the packages built is chosen automatically based on the version
used; a version with a `-` in it is considered a pre-release and will use the
`vcf-cli-unstable` package name, while other versions will use the
official `vcf-cli` package name.

The package built will automatically handle the installation of either
`amd64` or `arm64` Windows versions of the CLI based on the architecture
of the machine on which the package is run.

## Building the Chocolatey package

Executing the `hack/choco/build_package.sh` script will build the Chocolatey
package under `hack/choco/_output/choco`.

The `hack/choco/build_package.sh` script is meant to be run on a Linux machine
that has `choco` installed.  This is most easily done using docker.
To facilitate building the package, the new `choco-package`
Makefile target has been added; this Makefile target will first start a docker
container and then run the `hack/choco/build_package.sh` script.

NOTE: This docker image can ONLY be run on an AMD64 machine (even with emulation
of AMD64 on Mac, the chocolatey binary crashes when running an AMD64 docker image
on an ARM64 Mac).

```bash
cd vcf-cli
make choco-package
```

Note that the `hack/choco/build_package.sh` script automatically fetches the
required SHAs for the CLI binaries from the appropriate Github release.  If the
Github release is not public yet, it is possible to provide the SHA manually
through the environment variables `SHA_FOR_CHOCO_AMD64` and `SHA_FOR_CHOCO_ARM64`
as shown below:

```bash
cd vcf-cli
SHA_FOR_CHOCO_AMD64=1234567890 SHA_FOR_CHOCO_ARM64=0987654321 make choco-package
```

Note: It is not possible to publish the Chocolatey package before the release
is public on github because the publication testing done on the Chocolatey
community repo will fail when trying to install the package.

### Content of Chocolatey package

Currently, we build a Chocolatey package without including the actual VCF CLI
binary. Instead, when the package is installed, Chocolatey will download the
CLI binary from Github. This has to do with distribution rights as we will
probably publish the Chocolatey package in the community package repository.

## Testing the built Chocolatey package locally

Installing the VCF CLI using the newly built Chocolatey package can be done
on a Windows machine having `choco` installed. First, the Chocolatey package must
be manually uploaded to the Windows machine.

For example, if we upload the package to the Windows machine under
`$HOME\vcf-cli.0.90.1.nupkg`, we can then simply do:

```bash
choco install -s="$HOME" vcf-cli
```

It is also possible to configure a local repository containing the local package:

```bash
choco source add -n=local -s="file://$HOME"
choco install -s=local vcf-cli
```

### Installing a pre-release

To install a pre-release package, the same procedure must be used as described above
but for the actual installation the command should be:

```bash
choco install -s="$HOME" vcf-cli-unstable --pre
```

or

```bash
choco source add -n=local -s="file://$HOME"
choco install -s=local vcf-cli-unstable --pre
```

## Uninstalling the VCF CLI

To uninstall the VCF CLI after it has been installed with Chocolatey:

```bash
choco uninstall vcf-cli
```

or for pre-releases:

```bash
choco uninstall vcf-cli-unstable
```

## Publishing the package

The VCF CLI Chocolatey package is published to the main Chocolatey
community package repository under the `vmware-vcf` user account.
This step currently needs to be done manually by running the following
commands.  Note that the docker `chocolatey/choco:v1.4.0` needs to be
run under AMD64 for the `choco` command to work.

```bash
$ docker run --rm -it chocolatey/choco:v1.4.0
curl -sLO <URL of Choco package build>/chocorepo.tgz
tar xf chocorepo.tgz
# For final releases
choco push --source https://push.chocolatey.org/ --api-key <api-key> choco/vcf-cli.<version>.nupkg
# or for the vcf-cli-unstable package
choco push --source https://push.chocolatey.org/ --api-key <api-key> choco/vcf-cli-unstable.<version>.nupkg
```

The package will almost immediately become available for installation using
the `--version` flag.  However, for the package to become public and be installed
by default without the use of the `--version` flag, it may take a couple of days
as the package must be approved by a human maintainer of the Chocolatey project.

Progress can be monitored at the following URL (note that you need to be logged
in as vmware-vcf):

```bash
https://community.chocolatey.org/profiles/vmware-vcf
```

## Testing after publication

As soon as the `choco push` command is done, the package should be available
using the `--version` flag.  To install it please refer to
[the installation documentation](../../docs/quickstart/install.md#chocolatey-windows).
