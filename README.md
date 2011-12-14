# About

- - - - - -

### Overview
This sample module was designed to show how you can add customizations to an existing project based on the Argos SDK. This module was designed to supplement the [argos-saleslogix][argos-saleslogix] project.

### Included Examples
*  Adding a Quick Action to an existing view (Account Detail)
*  Add a field to existing detail and edit views (Account Detail/Edit)
*  Change a label on an existing view (Account Detail)
*  Hide a field on an existing view (Account Detail)
*  Add a custom Toolbar button to an existing view (Account Detail)
*  Override the layout template for a list view (Contact List)
*  Add a custom view that derives from the base view type (Google Map view)
*  Example of overriding CSS styling (sample.css)
*  A rudimentary Groups implementation using the Groups SData endpoint (GroupsList.js)
*  Show how to add a custom view (groups_list) to the "default" set of views displayed on the home screen.
*  Example of handling a self-join where only the ID is available (Parent in Account Detail/Edit)

#Installation

- - - - - 

### Prerequisites
*	A web server

### Clone repository
1.	Open a command prompt.
2.	change to the base directory where you cloned [Argos SDK][argos-sdk], eg:

		cd \projects\sage\mobile
3.	Execute the following commands (clone command shown with READ-ONLY URL; if you have commit rights, use the appropriate Read+Write URL).

		cd products
		git clone git://github.com/SageSalesLogix/argos-sample.git

    __Note:__ If you're downloading and extracting the zip file instead of using git directly, the top-level folder in your download will probably be named something like "SageSalesLogix-argos-sample-nnnnn". You'll want to rename this folder to argos-sample, and put it under your products sub-folder. You'll end up with a folder structure like this:

        ...\mobile\argos-sdk
        ...\mobile\products\argos-sample

### Setup and run the application in "debug" mode

1.	Follow the instructions for running the argos-saleslogix project in debug mode in that project's README.

2.  Make a copy of the argos-saleslogix index-dev.html file and name it index-dev-sample.html.

3.  Edit following lines to index-dev-sample.html. Note the relative paths pointing to the argos-sample folder. An example of this file is included with this project.

```
    require({
            baseUrl: "./",
            packages: [
            { name: 'dojo', location: '../../argos-sdk/libraries/dojo/dojo' },
            { name: 'dijit', location: '../../argos-sdk/libraries/dojo/dijit' },
            { name: 'Sage/Platform/Mobile', location: '../../argos-sdk/src' },
            { name: 'Mobile/SalesLogix', location: 'src' },
            { name: 'Mobile/Sample', location: '../argos-sample/src' }, // <-- Namespace and src folder path
            { name: 'configuration/sample', location: '../argos-sample/configuration' }, // <-- configuration/name, config folder path
            { name: 'localization/sample', location: '../argos-sample/localization' } // <-- localization/name and locale folder path
            ]
    });

    var application = 'Mobile/SalesLogix/Application',
        configuration = [
            'configuration/sample/development' //<-- development config file (no extension)
        ];
    require([application].concat(configuration), function(application, configuration) {
        var localization = [
            'localization/en',
            'localization/saleslogix/en',
            'localization/sample/en' // <-- locale file (no extension)
        ];
```

4.	Place index-dev-sample.html in the argos-saleslogix folder. In your browser, open index-dev-sample.html from the file system, or...navigate to the path `/mobile/products/argos-saleslogix/index-dev-sample.html` on your web server, eg:

		http://localhost/mobile/products/argos-saleslogix/index-dev-sample.html

### Building A Release Version

#### Before You Start

You may place information about your customization module in the `module-info.json` file in the root directory. This information will be displayed in Application Architect (in the next release) for easy identification and versioning.

#### Requirements
*	Windows

#### Steps
1.	Save this [gist](https://gist.github.com/815451) as `build-module.cmd` to the directory where you cloned [Argos SDK][argos-sdk] (The same folder where you created the Products folder).
2.	Open a command prompt and execute the following, changing paths as appropriate, eg:

        cd \projects\sage\mobile
        build-module sample

3.	The deployed module will be in a `deploy` folder in the directory where you cloned [argos-sample][argos-sample].

### Deploying

#### Setup
1.	Open the deploy folder for the product, eg:

		mobile\products\argos-sample\deploy

2. Then open the `module-fragment.html` file. This file will be placed into all the `index` files.

3. Edit it to point to your minified script and stylesheet (following the `deploy` folder layout):

```
    <!-- Sample -->
    <link type="text/css" rel="stylesheet" href="content/css/sample.css" />
    <script type="text/javascript" src="content/javascript/argos-sample.js"></script>
```    

4. At this point this guide will continue assuming you are manually deploying, this section will change when AA supports Mobile Deployment.

5. Copy all the folders within `deploy\argos-sample` (configuration, content and localization) and paste them into your Virtual Directory (SlxMobile) of your portal (where you deployed argos-saleslogix)

6. Edit `index.html`, `index-nocache.html`, `index.aspx` and `index-nocache.aspx` by copying the lines from `module-fragment.html` (the ones you added earlier) into each file at the designated modules marker:

```
    <!-- Modules -->
    <!--{{modules}}-->
```

To:

    <!-- Modules -->
    <!-- Sample -->
    <link type="text/css" rel="stylesheet" href="content/css/sample.css" />
    <script type="text/javascript" src="content/javascript/argos-sample.js"></script>


#### Finished

The argos-sample module will now be part of the SlxMobile client.


[argos-sdk]: https://github.com/Sage/argos-sdk "Argos SDK Source"
[argos-saleslogix]: https://github.com/SageSalesLogix/argos-saleslogix "Argos SalesLogix Source"
[argos-sample]: https://github.com/SageSalesLogix/argos-sample "Argos Sample"