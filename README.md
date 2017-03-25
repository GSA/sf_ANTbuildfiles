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
  your Salesforce org.  

Usage
---------------
Use CL or Git Bash and Run **``ant [target]``** from the ``deployment`` directory.


### Targets
Shorthand targets included in the build file.

#### deploy
This is a global target build to call out multiple short hand targets within the build.xml file. This target calls following targets
``retrieveunpackaged``
``retrieveunpackagedstatic``
``deployCodeVerify``
``deployCode``

Example:

   ```<target name="deploy">
   
	  <echo>Retrieving backup using the package.xml in "src"</echo>
        <antcall target="retrieveUnpackaged" />
	  <echo>Retrieving backup using the static/package.xml</echo>
        <antcall target="retrieveUnpackagedStatic" />
	  <echo>Performing code verification to the target sandbox</echo>
		  <antcall target="deployCodeVerify" />
	  <echo>Performing code Deployment to the target sandbox</echo>	
		  <antcall target="deployCode" />
    </target>```



#### retrieveUnpackaged
retrieve and unpackaged set of metadata from your org.

#### retrieveUnpackagedstatic
Retrieve an unpackaged set of metadata from your org. The file ``static/package.xml`` lists what is to be retrieved

#### deployCodeVerify
Validate the contents of the ``/src`` directory, running the tests for specified classes.

#### deployCode
Deploy the contents of the ``/src`` directory, running the tests for specified classes.

#### undeploy
Remove/Undeploy metadata specified in a ``destructiveChanges.xml`` file.



