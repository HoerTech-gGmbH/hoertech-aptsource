# hoertech-aptsource
The project in this git repository creates two debian packages: 
* `apt.hoertech`
* `aptdev.hoertech`

Each package installs a file in `/etc/apt/sources.list.d` which points to our
apt repository, either http://apt.hoertech.de/ or http://aptdev.hoertech.de.

Each package is created multiple times:
* For three target systems: `xenial-16.04`, `bionic-18.04`, and `focal-20.04`
* For two CPU architectures: `amd64` and `armhf`

So that in total 12 packages are created.

The packages `aptdev.hoertech` depend on the respective `apt.hoertech` package
(for the same CPU and target system), because some packages in our development
repository depend on packages only available in the stable repository.  
The stable repository only has dependencies on packages in the stable repository
itself or on standard ubuntu packages.

The `apt.hoertech` package also depends on a package containing our repository
signing key, `hoertech-openmha-keyring`.

The debian packages are created from template files (all files here whose name
begins with `template`) for all variants by the shell script
`create_debian_packages`.  Package `mhamakedeb` is a build dependency.

This repository is observed by our Jenkins server and rebuilt upon changes in
build job hoertech-tools/hoertech-aptsource.  See `Jenkinsfile`.

This repository is observed by our Phabricator in rAPTSRC.

When updating any file in this repository, then the version number in file
`version` should be updated as well.
