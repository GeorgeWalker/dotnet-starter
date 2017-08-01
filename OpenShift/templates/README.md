OpenShift Configuration and Deployment
----------------

The Tools project contains the Build Configurations (bc) which produce images sent to Image Streams (is) that are referenced by the Deployment Configurations.  The Tools project also contains the supporting infrastructure to perform the build.

Steps to configure the deployment:
----------------------------------

Ensure that you have access to the build and deployment templates.

These can be found in the `OpenShift/templates` folder of the project repository.

If you are setting up a local OpenShift cluster for development, fork the main project.  You'll be using your own fork.

Connect to the OpenShift server using the CLI; either your local instance or the production instance. 
If you have not connected to the production instance before, use the web interface as you will need to login though your GitHub account.  Once you login you'll be able to get the token you'll need to login to you project(s) through the CLI from here; Token Request Page.  The CLI will also give you a URL to go to if you attempt a login to the OpenShift server without a token.

The same basic procedure, minus the GitHub part, can be used to connect to your local instance.

Login to the server using the oc command from the page.
Switch to the Tools project by running:
`oc project <name of tools project>`

`oc process -f build-template.json | oc create -f -`

This will create the objects in OpenShift necessary to build the software.

You can now login to the OpenShift web interface and observe the progress of the initial build.

Deployment Environment Setup
---------------------------
The next step is to setup the deployment environments.  Examples of deployment environments are "DEV", "TEST", "PROD".  Some projects may have less or more deployment environments depending on the business needs of the project.

Deployment to the various environments is controlled through the build pipeline, as defined in the Jenkinsfile for the build pipeline.

To provision the deployment environment, execute the following commands:

- `oc project <deployment environment>`
- By default projects do not have permission to access images from other projects.  You will need to grant that.
Run the following:
- `oc policy add-role-to-user system:image-puller system:serviceaccount:<project_identifier>:default -n <project namespace where project_identifier needs access>`

  - EXAMPLE - to allow the production project access to the images, run:

  - `oc policy add-role-to-user system:image-puller system:serviceaccount:<project-name>-prod:default -n <project-name>-tools`

- Process and create the Environment Template
  - `oc process -f deployment-template.json  -p APP_DEPLOYMENT_TAG=<DEPLOYMENT TAG> | oc create -f -`
	- Substitute dev (dev environment), test (test environment) or prod (prod environment) for the <DEPLOYMENT TAG>
