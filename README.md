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

The following figure gives an overview of the architecture of the sample app:

![](https://github.com/opentdc/app-sample/blob/master/architecture-1.png)

### Service

* The service implements the API of the app as REST/JSON service. It
  offers all methods required by the Javascript GUI (in this case ./index.html).
* The service is implemented as a Java servlet, namely as JSP (./Api.jsp). The 
  JSP approach allows on-the-fly compiling and allows ultra-fast and flexible 
  development roundtrips.
  
The service implementation Api.jsp has the following layout:

	Api.jsp:
	
	   <%@page contentType="text/html;charset=UTF-8" language="java" pageEncoding="UTF-8" %>
	   <%!
	
	      // ContactModel bean
	      public static class ContactModel {
	         ...
	      }
			
	      public static ContactModel getContact(request, path) {
	         // delegate to backend
	      }
			
	      public static ContactModel createContact(request, path) {
	         // delegate to backend
	      }
			
	      public static ContactModel updateContact(request, path) {
	         // delegate to backend
	      }
			
	      public static List<ContactModel> findContacts(request, path, query) {
	         // delegate to backend
	      }

	   %>
	   <%
	   	* dispatch request and invoke methods
	   	* return result as JSON response 
	   %>

### GUI
The GUI is a standard webapp. It communicates with the service over REST/JSON.

Below is the screenshot of the sample app which allows to get, update and create
contacts using the APIs <code>provider/{pid}/segment/{sid}/contact/{cid}</code>
and <code>provider/{pid}/segment/{sid}/contact</code>.

![](https://github.com/opentdc/app-sample/blob/master/architecture-2.png)

### Backend

* The backend can be any database or application service (ERP, CRM, CM, DM, etc.).
  The service-tier delegates to the backend in order to store and retrieve data
  and execute business-logic. 
* The project app-generic offers a very simple file-based StoreManager which allows to
  store objects as JSON-formatted files. This allows to quickly build prototypes
  and proof-of-concepts. 

## WebApp Layout

The file layout of the webapp looks as follows:

		opentdc-app-sample
		   + WEB-INF
		     + web.xml
		   + index.html
		   + Api.jsp
		   + js
		   	+ bootstrap
		   	+ jquery
		   	
Of course, instead of bootstrap any other webapp framework can be used (Polymer, AngularJ, ...).
