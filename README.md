sf_ANTbuildfiles
=================

GSA Release Managment sample Salesforce.com deployment structure utilizing
[Apache Ant](http://ant.apache.org/) and the
[Force.com Migration Tool](https://developer.salesforce.com/page/Force.com_Migration_Tool).

This structure includes 
1.	``src`` folder that includes ``package.xml`` and ``sample components``
2.	 ``build.xml`` file with targets to easily interact with the Migration Tool targets 
3.	``build.properites`` file that includes Salesforce org information. 

This structure can be used as a base for your Salesforce deployments to quickly deploy metadata to your Salesforce org.

Getting Started
---------------

*System Requirements
1. **Apache Ant** - See [Installing Apache Ant](http://ant.apache.org/manual/install.html)
   for details.
2. **Force.com Migration Tool** - See
   [Installing the Force.com Migration Tool](http://www.salesforce.com/us/developer/docs/daas/Content/forcemigrationtool_install.htm)
   for details. 
3. After completing installations, you should have ``ant-salesforce.jar`` included in
   your Ant libraries.

###Contents
* **``undeploy``** - Sample structure for deleting files from a Salesforce
  org. Includes an empty ``package.xml`` and a ``destructiveChanges.xml``
  that lists the files to be deleted.
* **``unmanaged-pacakge-name``** - Sample files that make up an unmanaged
  package. The package name is defined in the ``fullName`` element of the
  ``package.xml``.
* **``unpackaged``** - Sample files that don't belong to a package.
* **``build.properties``** - Ant properties file for individual
  configurations (e.g. usernames and passwords).
* **``build.xml``** - Ant build file with shorthand targets to use the
  Force.com Migration Tool targets.
* **``manifiest.xml``** - Sample list of components used for retrieving
  Salesforce metadata.

###Configurables
List of configurable build properties from ``build.properties``:

* **``sf.username``** - Username for the org you will be deploying to /
  retrieving from.
* **``sf.password``** - Password + security token for the user you wish
  to login as for deploying/retrieving metadata.
* **``sf.serverurl``** - Login url for your Salesforce org type.  Prod/dev use
  <http://login.salesforce.com>, sandboxes use <http://test.salesforce.com>.
* **``deploy.dir``** - The directory containing the metadata to be deployed to
  your Salesforce org.  This folder includes a ``package.xml`` file that lists
  the metadata to be deployed.
* **``undeploy.dir``** - The directory containing the ``destructiveChanges.xml``
  file that lists the contents to be removed from your Salesforce org.
  Also contains an empty ``package.xml``.
* **``retrieve.dir``** - The directory to store metadata retrieved from your
  Salesforce org based on the contents of the ``manifiest.xml`` file.
* **``sf.packageName``** - Comma-separated list of package names to be retrieved
* **``sf.zipFile``** - Path of a zip file to be retrieved
* **``sf.metadataType``** = Metadata type name for bulk retrieval or listings

Usage
---------------
Run **``ant [target]``** from the ``deployment`` directory to utilize
the targets of the migration tool.

    Usage: ant [target]

    Available targets:
      deploy           Deploy contents of deploy.dir
      deployRunAll     Deploy contents of deploy.dir and run all tests
      deployZip        Deploy contents of sf.zipFile
      describe         Describe all metatdata types
      help, usage      Displays these usage guidelines
      list             List all information of items of metadata type
                       sf.metadataType
      retrieve         Retrieve contents of manifest.file
      retrieveBulk     Retrieve all instances of a given sf.metadataType
      retrievePackage  Retrieve contents of sf.packageName
      test             Test deploy contents of deploy.dir
      undeploy         Delete contents of destructiveChanges.xml

### Targets
Shorthand targets included in the build file.

#### deploy
Deploy unpacked metadata from specified ``deploy.dir`` directory. Optionally
specify which unit tests to run from this target.

#### deployRunAll
Deploy unpacked metadata from specified ``deploy.dir`` directory and run all
tests.

#### deployZip
Deploy a zip of metadata files specified in ``sf.zipFile`` to the org.

#### describe
Retrieve the information on all supported metadata types for your current org.

#### list
Retrieve the information of all items of a particular metadata type specified
by ``sf.metadataType``.

#### retrieve
Retrieve an unpackaged set of metadata from your org based on the contents of
``manifest.xml``.  Retrieved metadata is stored in the relative ``retrieve.dir``
directory.

#### retrieveBulk
Retrieve all the items of a particular metadata type defined by
``sf.metadataType``. Retrieved metadata is stored in the relative
``retrieve.dir`` directory.

#### retrievePackage
Retrieve metadata for all the packages specified under ``sf.packageName``.
Retrieved metadata is stored in the relative ``retrieve.dir`` directory.

#### test
Test deploy the contents of ``deploy.dir``.  This uses the provided username
and password and does a ``checkOnly`` deploy to your Salesforce org.

#### undeploy
Remove/Undeploy metadata specified in a ``destructiveChanges.xml`` file.



