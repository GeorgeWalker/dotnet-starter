dotnet-starter
-----------------
This project provides a baseline code base to help you kick start a dotnet core 2.0 project in OpenShift.

What you get
------------
- OpenShift templates for build and deployment
- Build template contents:
	- Imagestreams for the starter app and dependencies
	- A build config that produces a dotnet 2.0 S2I image from official sources using the RHEL7 base
	- A build config for an example API server
	- Deployment configurations, secret, route and persistent volumes to support a SonarQube installation, complete with Postgres database.
	- Build template contains the full Continuous Integration / Deployment Pipeline with the following stages:
		- Checkout source from Git
		- Build the product
		- Conduct functional tests (Behavior Driven Development) using the NavUnit / Geb framework
		- Promote to Test / Prod based on input
	- A complete SonarQube installation that can be used to monitor code quality
- Deployment template contents:
	- Deployment configuration for the application included in the build
	- A service that points to the application
	- A route that exposes the service

Development
-----------
This project uses .NET Core version 2, which is currently in Preview (3).  The type of application is a Model View Controller (MVC) web application.  Static files are supported as the MVC code.  An example REST interface to a test service is provided.

You will need to install Visual Studio 2017 Preview 3 in order to effectively develop the application from a Windows PC.

Note that .NET Core is cross platform, so you can also use a Mac or Linux computer equipped with the appropriate build tools.  

Static Code Analysis with SonarQube
-------------------------------------

SonarQube scans for C# currently require a Windows PC or server to run.  As such, they cannot be run from the Linux based OpenShift system.

Starting with dotnet core version 1.2, the .csproj project file format is used.  This project file format allows the use of MSBuild to compile the project, which is also a requirement for SonarQube.


Steps to conduct static code analysis:
1) Install the Visual Studio 2017 Community Edition plus standalone build tools, such that you are able to compile the source for the application.
2) Login to the sonar instance created during provisioning for your project
3) Aquire a token by going to My Account -> Security Tab
4) Change to the folder containing the .SLN file (the Server directory)
5) Edit the sonar.bat file in that folder, changing the token to match the value above.
6) Run sonar.bat on a Windows computer to execute the scan and upload the stats.

Contribution
------------

Please report any [issues](https://github.com/bcgov/dotnet-starter/issues).

[Pull requests](https://github.com/bcgov/dotnet-starter/pulls) are always welcome.

If you would like to contribute, please see our [contributing](CONTRIBUTING.md) guidelines.

Please note that this project is released with a [Contributor Code of Conduct](CODE_OF_CONDUCT.md). By participating in this project you agree to abide by its terms.

License
-------

    Copyright 2017 Province of British Columbia

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at 

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

Maintenance
-----------

This repository is maintained by BC Developer's Exchange
