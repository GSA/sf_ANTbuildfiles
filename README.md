sf_ANTbuildfiles
=================

GSA Release Managment sample Salesforce.com deployment structure utilizing
[Apache Ant](http://ant.apache.org/) and the
[Force.com Migration Tool](https://developer.salesforce.com/page/Force.com_Migration_Tool).

This structure can be used as a base for your Salesforce deployments to quickly deploy metadata to your Salesforce org.

Getting Started
---------------

#System Requirements
1. **Apache Ant** - See [Installing Apache Ant](http://ant.apache.org/manual/install.html)
   for details.
2. **Force.com Migration Tool** - See
   [Installing the Force.com Migration Tool](http://www.salesforce.com/us/developer/docs/daas/Content/forcemigrationtool_install.htm)
   for details. 
3. After completing installations, you should have ``ant-salesforce.jar`` included in
   your Ant libraries.

#Contents
* **``removecodepkg``** - Sample structure for deleting files from a Salesforce
  org. Includes an empty ``package.xml`` and a ``destructiveChanges.xml``
  that lists the files to be deleted.
* **``static``** - A static file is created and uploaded to the folder which contains metadata that will be retrieved for each deployment. In case of a package with only permissionsets the ‘retrieveunpackaged’target will just retrieve the ``<userpermission>`` as it is missing the supporting metadata while retrieving from the target org. Static package will ensure all the metadata components are included for a successful permissionset retrieve.
* **``src``** - Sample struture for deploying files to Salesforce Org. Inludes ``pckage.xml`` and components that are mentioned in the ``package.xml``
* **``build.properties``** - Ant properties file for individual
  configurations (e.g. usernames and passwords/sessionId).
* **``build.xml``** - Ant build file with shorthand targets to use the
  Force.com Migration Tool targets.


#Configurables
List of configurable build properties from ``build.properties``:

* **``sf.username``** - Username for the org you will be deploying to /
  retrieving from.
* **``sf.password``** - Password + security token for the user you wish
  to login as for deploying/retrieving metadata.
* **``sf.sessionId``** - Salesforce session Id for the user you wish 
  to login as for deploying/retrieving metadata. Session Id can be retrieved by using this command in the Devconsole : ``System.debug('The Session ID is ' + UserInfo.getSessionId());``
* **``sf.serverurl``** - Login url for your Salesforce org type.  Prod/dev use
  <http://login.salesforce.com>, sandboxes use <http://test.salesforce.com>.
* **``sf.deployRoot``** - The directory containing the metadata to be deployed to
  your Salesforce org.  This folder includes a ``package.xml`` file that lists
  the metadata to be deployed.

Usage
---------------
Run **``ant [target]``** from the ``deployment`` directory.


### Targets
Shorthand targets included in the build file.

#### deploy
Deploy unpacked metadata from specified ``deploy.dir`` directory. Optionally
specify which unit tests to run from this target.

#### retrieveUnpackaged
Deploy unpacked metadata from specified ``deploy.dir`` directory and run all
tests.

#### retrieveUnpackagedstatic
Deploy a zip of metadata files specified in ``sf.zipFile`` to the org.

#### deployCodeVerify
Retrieve the information on all supported metadata types for your current org.

#### deployCode
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



