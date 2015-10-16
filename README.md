# app-sample

## Build

Prerequisites:

* JDK 7 must be installed
* ant must be installed

		cd app-sample
		ant clean
		ant assemble


This builds the following WARs located jre-1.7/app-sample/deployment-unit/:

* opentdc-app-sample.war: sample app which demonstrates basic principals
  of how opentdc apps are built.


## Deploy

Copy the opentdc-app-sample.war manually to the webapps directory of Tomcat and launch
the app with the URL http://localhost:8080/opentdc-app-sample/.


## Architecture

The following figure gives an overview of the architecture of the app


* The backend of the app is implemented as a Java servlet, namely as JSP
  (./Api.jsp). The JSP approach allows on-the-fly compiling of the backend and 
  allows ultra-fast and flexible development roundtrips. There is no need for 
  recompiling Java classes, etc.
* The backend implements the API of the app as REST/JSON service. Therefore it 
  offers all methods required by the Javascript GUI (in this case ./index.html).
* Objects are stored in JSON-format as files in the webapp directory /data. Files
  can be created, updated and removed manually as required. The file-based
  StoreManager is quite fault-tolerant. IMPORTANT: DO NOT USE the file-based 
  StoreManager in production.  
