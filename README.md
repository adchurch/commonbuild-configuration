# commonbuild-configuration
This repository contains configuration data used by the [commonbuild continuous integration (CI) system](https://github.com/ni-veristand-cds/commonbuild). **configuration.toml** contains configuration data for the GitHub organization in which it is located. This repository must be located in the same GitHub organization as a copy of the commonbuild library repository as well as the repositories for the projects being built. 
### Using this Repository
This repository tracks the build number for each repository in this GitHub organization. The build numbers are stored in the **configuration.toml** file in the top level of this repository. 

For example, if the last build of the XYZ Custom Device for VeriStand 2017 was 10 and its repository is named XYZ-Custom-Device, then **configuration.toml** would contain:

    [repositories.XYZ-Custom-Device]
    2017_build_version = 10


The commonbuild CI system will store the most recent build number for each project in this repository. The CI system will only update the build number after a successful build. The build number will be incremented by successful builds in any branch within the XYZ-Custom-Device project repository.

The CI system will attempt to read the latest build number from this repository. If a project is not found then it will be added to **configuration.toml** with its build number initialized to zero. 