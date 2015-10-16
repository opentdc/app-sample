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

The following figure gives an overview of the architecture of the app:

![](https://github.com/opentdc/app-sample/blob/master/architecture-1.png)

### Service

* The service implements the API of the app as REST/JSON service. It
  offers all methods required by the Javascript GUI (in this case ./index.html).
* The service is implemented as a Java servlet, namely as JSP (./Api.jsp). The 
  JSP approach allows on-the-fly compiling of the backend and allows ultra-fast 
  and flexible development roundtrips.

### GUI
The GUI is a standard webapp. It communicates with the service over REST/JSON.

### Backend

The backend can be any database or application service (ERP, CRM, CM, DM, etc.).
The service-tier delegates to the backend in order to store and retrieve data
and execute business-logic. The project app-generic offers a very simple file-based StoreManager which allows to store objects as JSON-formatted files.

