# Java-Based-Web-Service-Framework
This framework makes it easy to create services with less efforts. User can easily use the framework to produce backend services of the web applications/projects.

You can use this framework to create backend/serverside services for web requests, Now user not need to know about servlets or edit web.xml file,user can simply use the framework and all its need can be solved.
## Overview

This framework provides following functions:

* No need for xml configuration.

* No need to write servlets classes for every new web request.

* User dont have to worry about get/post request and how to handle them.

* User dont have to worry about how to handle multipart request and how to parse them and process them in case of File Upload.

* User can use [GenerateService](generate/GenerateService.class) tool for find list of services and errors in services.

## Before you begin

* Download this git repositorie.

* Extract the zip file.

* Copy/Move the [packagePaths.path](WEB-INF/paths/packagePaths.path) file to tomcat9/webapps/"Your Project Name"/WEB-INF/paths/packagePaths
  packagePaths contains a json string storing list of package paths to where the services which are using this Framework exists : 
```  
{
  "listOfPaths":[ "/usr/local/tomcat9/webapps/"Your Project Name"/WEB-INF/classes",]
}
```

the above example show how to list paths to all the places where services classes are located (services classes are classes using the framework to create web service for requests).

* Copy/Move web.xml to tomcat9/webapps/"Your Project Name"/WEB-INF/.
  Now you can not forget about web.xml as you don't have to change or configure it again.
  
* Now copy [webServiceFramework.jar](webServiceFramework.jar) to tomcat9/Webapps/"Your Project Name"/WEB-INF/lib/.
  Tomcat search for servlet classes in classes folder or lib folder.

* Now copy all files inside [WEB-INF/lib](WEB-INF/lib) folder and paste them inside tomcat9/lib/.
  these are all the files you will ever need to create a web service.Our framework is dependent on some of the these           files.

* Now Move the generate and images directory inside your project directory parallel to WEB-INF directory.It's help to           generate services and errors pdfs.

* You are done setting up the environment,now you can use the frameWork easily.
