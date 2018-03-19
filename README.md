# commonbuild-configuration
### Overview
This repository contains configuration data used by the [commonbuild continuous integration (CI) system](https://github.com/ni-veristand-cds/commonbuild). 

**Configuration.toml** contains configuration data for the GitHub organization in which this repository is located. This repository must be located in the same GitHub organization as a copy of the commonbuild library repository as well as the repositories for the projects being built. 
### Using this Repository
This repository tracks configuration data for each repository in this GitHub organization. Currently only the build numbers and GitHub release configuration are stored in the **configuration.toml** file.

All configuration data for a given repository is stored under a repository object in **configuration.toml**. 
For example, configuration data for **XYZ Custom Device** located at **http:\\www.github.com\ThisOrg\xyz-custom-device** would be present in **configuration.toml** under:


    [repositories.my-custom-device]


#### Using the repository build number configuration 
For example, if the last build of the XYZ Custom Device for VeriStand 2017 was 10 and its repository is named XYZ-Custom-Device, then **configuration.toml** would contain:

    [repositories.XYZ-Custom-Device]
    2017_build_version = 10


The commonbuild CI system will store the most recent build number for each project in this repository. The CI system will only update the build number after a successful build. The build number will be incremented by successful builds in any branch within the XYZ-Custom-Device project repository.

The CI system will track build numbers for different year versions independently. 

The CI system will attempt to read the latest build number from this repository. If a build number for the current project and year version is not found then it will be added to **configuration.toml** with its build number initialized to zero. 

#### Using the repository GitHub release configuration settings
The **configuration.toml** file is also used to configure whether the CI system will push built .nipkg files to the repository's GitHub Releases page:

*http:\\www.github.com\ThisOrg\xyz-custom-device\releases*  

To configure the CI system to push releases to GitHub you must specify which branches should be pushed for each year version. For example, to push 2017 releases to GitHub for the Master and Develop branches add the following to **configuration.toml** :

    [repositories.XYZ-Custom-Device]
    2017_build_version = 10
    2017_release_branches = ["master", "develop"]