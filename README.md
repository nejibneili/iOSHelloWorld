[![Build Status - Master](https://travis-ci.org/IBM-Bluemix/swift-helloworld.svg?branch=develop)](https://travis-ci.org/IBM-Bluemix/swift-helloworld)
![macOS](https://img.shields.io/badge/os-macOS-green.svg?style=flat)
![Linux](https://img.shields.io/badge/os-linux-green.svg?style=flat)

#Swift HelloWorld App Overview
This project contains a simple Swift hello world application that can be deployed to Bluemix or run locally on your [macOS](http://www.apple.com/osx/) or [Ubuntu Linux](http://www.ubuntu.com/download) system.  This sample application creates a basic server that returns an HTML greeting to the client.  Please note that this is not a production-ready application.  Instead, it is for educational purposes to learn about the types of applications you can develop using the Swift programming language.

## Application Requirements
To compile and run this sample application on your system, you need to install the [Swift compiler](https://swift.org/download/) for your platform. Please note that the Swift language is evolving and changing rapidly. The latest version of this Swift application works with the `3.0.1` version of the Swift binaries. You can download this version of the Swift binaries by following this [link](https://swift.org/download/).

If you are interested in manually deploying the application to Bluemix, you'd need to install the Cloud Foundry [command line](https://docs.cloudfoundry.org/devguide/cf-cli/install-go-cli.html) on your system.  Once it is installed, you can use it to [authenticate and access](https://www.ng.bluemix.net/docs/starters/install_cli.html) your Bluemix organization(s) and spaces.  You can find further details on how to deploy this sample application to Bluemix in the following sections.

## Run the app locally
Once you have installed the Swift compiler and cloned this Git repo, you can now compile and run the application. Go to the root folder of this repo on your system and issue the following command:
```
$ swift build
```
You should see an output similar to the following:
```
Compile Swift Module 'SwiftyJSON' (2 sources)
Compile Swift Module 'CloudFoundryEnv' (7 sources)
Compile Swift Module 'Utils' (6 sources)
Compile Swift Module 'Server' (1 sources)
Linking .build/debug/Server
```
Once the application is successfully compiled, you can run the executable that was generated by the Swift compiler:
```
$ .build/debug/Server
```
You should see an output similar to the following:

```
Server is listening on port: 8090
```

To connect to the server, you can use the browser of your preference (e.g. Firefox, Chrome, etc.) to point to the following URL: `http://<hostname>:8090/`, where `<hostname>` is the hostname or the IP address of the system where you are running the sample app.  If the browser is running on the same system, you can use localhost as the value for the hostname.  After you access the server, the browser should render an HTML page with the following message:

```
Hello from Swift on Linux!
```

Below the greeting message, you should also see an HTML table that displays the environment variables for the app.

## Running the app on Bluemix
### Using the magical button
Click the magical button below to automatically deploy this sample application to Bluemix.

[![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy)

When automatically deploying to Bluemix, the manifest.yml file [included in the repo] is parsed to obtain the name of the application.  For further details on the structure of the manifest.yml file, see the [Cloud Foundry documentation](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#minimal-manifest).

### Using the Cloud Foundry command line
You can also manually deploy the app to Bluemix.  Though not as magical as using the Bluemix button above, manually deploying the app gives you some insights about what is happening behind the scenes.  Remember that you'd need the Cloud Foundry [command line](https://www.ng.bluemix.net/docs/starters/install_cli.html) installed on your system to deploy the app to Bluemix.

Using the Cloud Foundry command line you can get a list of the buildpacks (along with their versions) that are installed on Bluemix.

```
cf buildpacks
```

Executing the above command should result in output similar to the following:

```
Getting buildpacks...

buildpack                              position   enabled   locked   filename
liberty-for-java                       1          true      false    buildpack_liberty-for-java_v3.3-20160912-1729.zip
sdk-for-nodejs                         2          true      false    buildpack_sdk-for-nodejs_v3.7-20160826-1101.zip
dotnet-core                            3          true      false    buildpack_dotnet-core_v1.0-20160826-1345.zip
swift_buildpack                        4          true      false    buildpack_swift_v2.0.0-20160915-1220.zip
java_buildpack                         5          true      false    java-buildpack-v3.6.zip
ruby_buildpack                         6          true      false    ruby_buildpack-cached-v1.6.16.zip
nodejs_buildpack                       7          true      false    nodejs_buildpack-cached-v1.5.11.zip
go_buildpack                           8          true      false    go_buildpack-cached-v1.7.5.zip
python_buildpack                       9          true      false    python_buildpack-cached-v1.5.5.zip
php_buildpack                          10         true      false    php_buildpack-cached-v4.3.10.zip
xpages_buildpack                       11         true      false    xpages_buildpack_v1.1.1-20160518-0936.zip
staticfile_buildpack                   12         true      false    staticfile_buildpack-cached-v1.3.6.zip
binary_buildpack                       13         true      false    binary_buildpack-cached-v1.0.1.zip
xpages_buildpack_v1_0_0-20160310-144   14         true      false    xpages_buildpack_v1.0.0-20160310-1442.zip
swift_buildpack_v1_1_1                 15         true      false    swift_buildpack-cached-v1.1.1.zip
dotnet-core_v0_9-20160706-1603         16         true      false    buildpack_dotnet-core_v0.9-20160706-1603.zip
sdk-for-nodejs_v3_7-20160823-1528      17         true      false    buildpack_sdk-for-nodejs_v3.7-20160823-1528.zip
liberty-for-java_v3_2-20160822-2200    18         true      false    buildpack_liberty-for-java_v3.2-20160822-2200.zip
swift_buildpack_v1_1_6-20160729-1205   19         true      false    buildpack_swift_v1.1.6-20160729-1205.zip
```

Looking at the output above, we can see that the Swift buildpack (v2.0.0) is installed on Bluemix.  This will allow a seamless deployment of the starter application to Bluemix. After you have cloned this Git repo, go to its root folder on your system and issue the following command Cloud Foundry command:

```
cf push
```

Executing the Cloud Foundry push command will parse the contents of the `manifest.yml` file and upload the application to Bluemix. The following is example output from executing the `cf push` command on the Swift `3.0` version of this application:

```
Using manifest file /Users/olivieri/git/swift-helloworld/manifest.yml

Creating app swift-helloworld in org roliv@us.ibm.com / space dev as roliv@us.ibm.com...
OK

Creating route swift-helloworld-nontanning-typhoon.stage1.mybluemix.net...
OK

Binding swift-helloworld-nontanning-typhoon.stage1.mybluemix.net to swift-helloworld...
OK

Uploading swift-helloworld...
Uploading app files from: /Users/olivieri/git/swift-helloworld
Uploading 35.3K, 17 files
Done uploading               
OK

Starting app swift-helloworld in org roliv@us.ibm.com / space dev as roliv@us.ibm.com...
-----> Downloaded app package (16K)
-----> Default supported Swift version is 3.0
-----> Installing system level dependencies...
-----> Installing libblocksruntime0_0.1-1_amd64.deb
-----> Installing libblocksruntime-dev_0.1-1_amd64.deb
-----> Installing libcurl3_7.35.0-1ubuntu2.6_amd64.deb
-----> Installing libkqueue0_1.0.4-2ubuntu1_amd64.deb
-----> Installing libssl-dev_1.0.1f-1ubuntu2.19_amd64.deb
-----> Installing openssl_1.0.1f-1ubuntu2.19_amd64.deb
-----> Installing uuid-dev_2.20.1-5.1ubuntu20_amd64.deb
-----> No Aptfile found.
-----> Writing profile script...
-----> Buildpack version 2.0.0
-----> Installing Swift 3.0
       Downloaded Swift
-----> Installing Clang 3.8.0
       Downloaded Clang
-----> This buildpack does not add libdispatch binaries for swift-3.0 (note: Swift binaries from 8/23 and later already include libdispatch)
-----> Building Package...
       Cloning https://github.com/IBM-Swift/Swift-cfenv.git
       HEAD is now at 04d7d88 Update swift version to 3.0
       Resolved version: 1.7.0
       Cloning https://github.com/IBM-Swift/SwiftyJSON.git
       HEAD is now at 73b523a 3.0
       Resolved version: 14.2.0
       Cloning https://github.com/IBM-Swift/BlueSocket.git
       HEAD is now at fc56939 Update to latest (9/16) toolchain
       Resolved version: 0.11.7
       Compile Swift Module 'Socket' (3 sources)
       Compile Swift Module 'SwiftyJSON' (2 sources)
       Compile Swift Module 'CloudFoundryEnv' (7 sources)
       Compile Swift Module 'Utils' (3 sources)
       Compile Swift Module 'Server' (1 sources)
       Linking ./.build/release/Server
-----> Copying dynamic libraries
-----> Copying binaries to 'bin'
-----> Cleaning up build files
-----> Cleaning up cache folder

-----> Uploading droplet (11M)

1 of 1 instances running

App started


OK

App swift-helloworld was started using this command `Server`

Showing health and status for app swift-helloworld in org roliv@us.ibm.com / space dev as roliv@us.ibm.com...
OK

requested state: started
instances: 1/1
usage: 128M x 1 instances
urls: swift-helloworld-nontanning-typhoon.stage1.mybluemix.net
last uploaded: Tue Sep 20 17:49:50 UTC 2016
stack: cflinuxfs2
buildpack: swift_buildpack

     state     since                    cpu    memory          disk        details
#0   running   2016-09-20 12:51:08 PM   0.0%   14.6M of 128M   36M of 1G
```

Once the sample application is pushed to Bluemix, you can access it using its route. You can log on to your [Bluemix account](https://console.ng.bluemix.net) to find the route of your application or you can inspect the output from the execution of the `cf push` command.  The string value (e.g. swift-helloworld.mybluemix.net) shown next to the urls should contain the route.  Use that route as the URL to access the sample server using the browser of your choice.  The browser should render an HTML page with the following message at the top:

```
Hello from Swift on Linux!
```

## Using a different version of Swift on Bluemix for your application
If you look closely at the output above returned by the `cf push` command, you will notice that `3.0` was the Swift version used for compiling and running the sample app on Bluemix.  If you have a Swift application that compiles with a different version of the Swift binaries, say `DEVELOPMENT-SNAPSHOT-2016-08-30-a`, you'd need to update the contents of the `.swift-version` file to:

```
DEVELOPMENT-SNAPSHOT-2016-08-30-a
```

After updating the `.swift-version` file, you can run the `cf push` command to push your application to Bluemix and use the specified version of the Swift binaries for compiling and running your application.

For a complete list of the Swift versions currently supported by the Swift buildpack for Bluemix, see the buildpack's [manifest](https://github.com/IBM-Swift/swift-buildpack/blob/bluemix-buildpack/manifest.yml) file.  If you cannot find the version of the Swift binaries you are looking for in this file, then that version is not currently supported.

```
Running the application in an IBM Container on Bluemix
```

This sample application can also be run in an IBM Container in Bluemix. For details on how to do this, see the [10 Steps To Running a Swift App in an IBM Container] (https://developer.ibm.com/swift/2016/02/22/10-steps-to-running-a-swift-app-in-an-ibm-container) blog post. There, you will find the necessary steps for creating an IBM Container that executes this starter application.
