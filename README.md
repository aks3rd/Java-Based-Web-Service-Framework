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

  the above example show how to list paths to all the places where services classes are located (services classes are classes   using the framework to create web service for requests).

* Copy/Move web.xml to tomcat9/webapps/"Your Project Name"/WEB-INF/.
  Now you can not forget about web.xml as you don't have to change or configure it again.
  
* Now copy [webServiceFramework.jar](webServiceFramework.jar) to tomcat9/Webapps/"Your Project Name"/WEB-INF/lib/.
  Tomcat search for servlet classes in classes folder or lib folder.

* Now copy all files inside [lib](lib) folder and paste them inside tomcat9/lib/.
  these are all the files you will ever need to create a web service.Our framework is dependent on some of the these           files.

* Now Move the generate and images directory inside your project directory parallel to WEB-INF directory.It's help to           generate services and errors pdfs.

* You are done setting up the environment,now you can use the frameWork easily.

## Tutorials and reference documentation

  User can create web service by using these annotations on class and Methods. User dont have to worry about how these         webservices will run when request arrives. User can request Data, HttpServletRequest and httpServletResponse from             framework.

## Annotations User can use are:

* @Path("/Test")
  Path annotation can be applied to class and method.value of path should starts with frount Slash followed by path.
  Example :
  ```
  import com.thinking.machines.annotations.*;
  @Path("/Test")
  public class Test
  {
   @Path("/doSomething")
   public String doSomething()
   {
    return "Cool Stuff";
   }
  }
  ```
  user can access this service by sending request to service/Test/doSomething.

* @RequestData("name")
  user can use the following annotation to request data from framework which arrives as web request.
  framework finds the value of the annotation an search for data with given name in request Bag and if found provide this     requestded data to user without user having to worry about conversions 
  Example :
  ```
  import com.thinking.machines.annotations.*;
  @Path("/Test")
  public class Test
  {
   @Path("/addData")
   public String addData(@RequestData("rollNumber")int rollNumber,@RequestData("name")String name)
   {
     System.out.println("Sucess");
     return "Data Saved";
   }
  }
  ```
 Example url to access add service 
 http://localhost:8080/webService/service/Test/addData?rollNumber=123&name=Akash+Soni

* @Secured(value="")
  By using this annotation user dont have to write verification code for every service that need to be secured,user can just   apply this annotation to all the services that are needed to be secured from unidentified access. 
  Example :
  ```
  import com.thinking.machines.annotations.*;
  @Path("/Test")
  public class Test
  {
   @Path("/delete")
   @Secured("full classname to your verification class")
   @ResponseType("text/html")
   @Forward("index.jsp")
   public String delete()
   {
    	return "Delete model service used";
   }
  }
  ```
  value of Secured annotation should be a full name to the actual class that verify user based on the users details.
  for this your verification class have to implement com.thinking.machines.interfaces.Security Inerface of the Framework       Module com.thinking.machines.interfaces.Security;

* @Forward("/index.jsp")
  Using this annotation user can forward request to another web service or to some jsp file
  above example show how to use forward annotaton to forward request to index.jsp,you can also forward to some other service   also.by giving service path as value of forward annotation.
  Example :
  ```
  import com.thinking.machines.annotations.*;
  @Path("/Test")
  public class Test
  {
   @Path("/delete")
   @Secured("full classname to your verification class")
   @ResponseType("text/html")
   @Forward("index.jsp")
   public String delete()
   {
    	return "Delete model service used";
   }
  }
  ```
* @ResponseType("json")
  User can specify what type of response it wants to send as a response for the request.
  user can choose three of the value as a response "json", "text/html" ,"nothing"
  if ResponseType annotation is not used then default response is text/html.
  example is shown above.

* If user send raw data in post Request user can just  use it simply as:-
  ```
  @Path("/add")
  @ResponseType("json")
  public Student add(Student s)
  {
	  return s;
  }
  ```
  Framework will automaically find the type of patameter and parse the raw data into Student object and pass it as argument   when invoking this service method

  After Creating all the services user can use [GenerateService](generate/GenerateService.class) of the Framework to create   two files service.pdf and errors.pdf
  [GenerateService](generate/GenerateService.class) will analyse all the service and create these pdf .
  service.pdf contains all the details of the unique services .
  errors.pdf will contain all the errors and mistakes done by user in creating the services and thus user can fix the error   before hand.
  java -classpath "path to Frame work jar";"path to tomcat lib for dependencies";. [GenerateService](generate/GenerateService.class) "path where you want to save those pdf files".
