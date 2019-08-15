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

### Converted Content Packages not Launching

* Branch: **issue/cp-not-launching**
* Ticket: none so far
* Temporary Fix: none
* Issues: After building (first **test-package** then root project
and launching the project the /system/console/osgi-installer will report
that CP is a **Untransformed Resource**.

#### Project Dependencies

* Build **sling-slingfeature-maven-plugin** branch **master**

The rest of the dependencies are either publicly available or they
provided by the project-local repo (folder **repository**)

#### Test Run

Build the project this way:
```
cd test-package
mvn clean install
cd ..
mvn clean install -P launch
```
Wait until Sling is up and running then go to:
```
http://localhost:8080/system/console/osgi-installer
```
The test package converted ui.apps is listed as **Untransformed Resources**. 
