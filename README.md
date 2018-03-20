# commonbuild-configuration
### Overview
This repository contains configuration data used by the [commonbuild continuous integration (CI) system](https://github.com/ni-veristand-cds/commonbuild). 

The configuration files in this repository contain build configuration data for the projects in this GitHub organization. This repository must be located in the same GitHub organization as a copy of the commonbuild library repository as well as the repositories for the projects being built. 
### Using this Repository
This repository contains a configuration file for each year version of VeriStand. Currently only the build numbers and GitHub release configuration are stored in the **configuration_201x.toml** files.

All configuration data for a given repository and year version of VeriStand is stored under a repository object in a **configuration_201x.toml** file. 
For example, configuration data for **XYZ Custom Device** for VeriStand 2015 located at *http://www.github.com/ThisOrg/xyz-custom-device* would be present in **configuration_2015.toml** under:

    [repositories.xyz-custom-device]
Repository names are **case sensitive**.

#### Using the repository build number configuration 
The commonbuild CI system will store the most recent build number for each project in this repository.

For example, if the last build of the XYZ Custom Device for VeriStand 2017 was 10 and its repository is named XYZ-Custom-Device, then **configuration_2017.toml** would contain:

    [repositories.XYZ-Custom-Device]
    build_version = 10


The CI system will only update the build number after a successful build. The build number will be incremented by successful builds in any branch within the XYZ-Custom-Device project repository.

The CI system will track build numbers for different year versions independently. 

The CI system will attempt to read the latest build number from this repository. If a build number for the current project and year version is not found then it will be added to **configuration_201x.toml** with its build number initialized to zero. 

#### Using the repository GitHub Release configuration settings
The **configuration_201x.toml** file is also used to configure whether the CI system will push built .nipkg files to the repository's GitHub Releases page:

*http://www.github.com/ThisOrg/xyz-custom-device/releases*  

To configure the CI system to push releases to GitHub you must specify which branches should be pushed for each year version. For example, to push 2017 releases to GitHub for the Master, Develop, and ABC branches of XYZ Custom Device the **configuration_2017.toml** file would include:

    [repositories.XYZ-Custom-Device]
    build_version = 10
    release_branches = ["master", "develop", "ABC"]
    
Branch names are **case sensitive**.
    
##### Version Conventions
The CI system will format nipkg version numbers according to the following patterns. The version convention roughly follows [Semantic Versioning 2.0.0](https://semver.org/). 
1. "master" Branch:
        MAJOR.MINOR.PATCH+BUILD
2. "develop" Branch:
        MAJOR.MINOR.PATCH-beta+BUILD
3. "ABC" Branch:
        MAJOR.MINOR.PATCH-alpha+BUILD
Where ABC is any arbitrary branch name.

        