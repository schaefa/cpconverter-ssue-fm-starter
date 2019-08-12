# Test Project to Showcase CP Converter Issues

This page contains instructions on how to build and run the Test Project
and what issues we see.
The launch will eventually fail as the aem-groovy-console will not run
on Sling but that is not the goal.

## Preparation

The test project depends on certain code bases which are mention below.
These must be built ahead of compiling this project.

## Branches

The project contains multiple branches to showcase the various issues
where some of the issues are manually fixed to move ahead.

### Package Group vs. Maven Group Issue

* Branch: **issue/package-group**
* Ticket: [SLING-8626][SLING-8626]
* Temporary Fix: maven the package group the same name as the Maven group
* Issues:
1. The converter's convert() method is not returning feedback on where it
placed the files and so it is very difficult to automate the installation
of the converted files into the local Maven repository
2. Because the CP Converter uses the package group and that one is
different from the Maven group the Sling FM Plugin will look up the
converted dependency in the package group path but the POM of that file
is in the Maven group path which causes conflicts in the Sling FM Plugin

#### Project Dependencies

* Build **sling-slingfeature-maven-plugin** branch **issues/SLING-8626**

The rest of the dependencies are either publicly available or they
provided by the project-local repo (folder **repository**)

#### Test Run

After the project dependencies are built you can run this test with:
```
mvn clean install
```
The first run will fail because of an issue with the Sling Feature Maven
Plugin that does not recognize generated FM files.
Executing
```
mvn clean install
```
will finally show this issue:
```
[ERROR] Failed to execute goal on project org.apache.sling.cpconverter.issue: 
Could not resolve dependencies for project 
org.apache.sling:org.apache.sling.cpconverter.issue:slingosgifeature:1.0.0-SNAPSHOT: 
Could not find artifact test-group:ui.apps:zip:cp2fm-converted:1.0.0-SNAPSHOT 
in apache.snapshots (https://repository.apache.org/snapshots) -> [Help 1]
```

[SLING-8626]: https://issues.apache.org/jira/browse/SLING-8626

## Run Test Project

### Prepare

All plugin and dependencies of not released code is incorporated into a
project local project as well as the Sling Starter Provisioning Model
so no further preparations are necessary.

### Build and Launch

This project is built with standard Maven command:
```
mvn clean install
```

To launch it just add the **launch** profile:
```
mvn clean install -P launch
```

Sling will start but you will see many dependency issues but as long as
Sling starts we are good here.
