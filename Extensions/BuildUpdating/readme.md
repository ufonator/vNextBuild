### Releases
- 1.0.x - Initial release
- 1.1.x - Logic fixed for updating
- 1.2.x - Added boolean to allow use of default build agent creditials
- 1.3.x - Fixed bug with handling of defaultcreds

A set of tasks to manage builds, it is assumed these tasks will usually be called from a release pipeline.

## Included Tasks
### Build Retension Task
This task sets the 'keep forever' retension flag on a build. It takes one parameter, the build selection mode, set to either:

* Select only the primary build associated with the release (default)
* All the build artifacts associated with the release
* (Advanced) Use use build agents default credentials as opposed to agent token - usually only every needed for TFS usage 

### Update Build Variable Task
This task allows a variable to be set in a build definition. 

The prime use of this task is envisaged to be the updating of a variable that specifies a version number that needs to be incremented when a release to production occurs.

It uses the following parameters

* Build selection mode 
    * Only the primary build associated with the release (default)
    * All the build artifacts associated with the release
* Variable name to update
* Method to update the variable
    * Auto-increment the variable (default)
    * Specify a value
* Value if not set to auto-increment
* (Advanced) Use use build agents default credentials as opposed to agent token - usually only every needed for TFS usage 

**Important**: The default rights of a build agent running a release is to not have the permission to edit the build definition. If this task is used without altering these permission you will get a 403 error

  
> Exception calling "UploadString" with "3" argument(s): "The remote server returned an error: (403) Forbidden." 


To address this problem

1. In a browser select the Build tab
2. Select 'All build definitions', right click and select security
3. Pick the user 'Project Collection Build Service (<a name>)' and make sure they have the 'Edit build definitions right set'