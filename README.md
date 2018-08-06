# SSL-Guide
Basic Tutorial that teaches you how to set up a secure SSL with Liberty

## Step I: set up a basic liberty server

### Using Terminal 

Clone from the follow repositorary: https://github.com/IBM-Cloud/java-helloworld.git

We utilize Maven to build this project. Please refer to the [Maven Website](http://maven.apache.org/) for instructions on how to donwload maven onto your computer.
**cd** into the java-helloworld folder, then issue the command **mvn clean install** to create the /target/JavaHelloWorldApp.war file.  
You should see the following output: 
[INFO] Packaging webapp
[INFO] Assembling webapp [JavaHelloWorldApp] in [/Your-Directory/java-helloworld/target/JavaHelloWorldApp-1.0-SNAPSHOT]
[INFO] Processing war project
[INFO] Copying webapp resources [/Your-Directory/java-helloworld/src/main/webapp]
[INFO] Webapp assembled in [24 msecs]
[INFO] Building war: /Your-Directory/java-helloworld/target/JavaHelloWorldApp.war
while you are in the java-helloworld folder, run **mvn liberty:run-server** to start up the server. Make sure you do not have a running application using *Port:9080* 

#### Using Eclipse 


Servlet.java: 
  annotation: @servletSecurity @HttpConstraint 
  commented out basicAuthenticationMechanism
  for transportGuarantee, specify the path as javax.servlet.annotation.ServletSecurity.TransportGuarantee.CONFIDENTIAL
    (might be unnecessary, need testing)
  
index.html
  href: redirect to servlet or adminonly from server.xml
  
bootstrap.properties
  default http/https port location and context root
  
server.xml
  keyStore: default id and password
  basicRegistry: show user(name), user password, group(admin/user)
  httpEndpoint: called from bootstrap
  webApplcation: where the Servlet is stored (war file)
  traceSpecification: enable trace functionality
  
web.xml
  added the security constraint: transport guarantee confidential 

"/finish/target/liberty/wlp/usr/servers/defaultServer/resources/security"
  removed the key 
  
how it works:
  The client(browser/website) wants to access Liberty. key.jks is a self-signed SSL certificate. When the client visits Liberty, it checks its certificate with list of trusted CAs. In this case, since the cerificate was self-signed, we need to add a browser exception sayign that we trust this entity. 
  
what is mutual connection? 
  The website has its certificate attached to it. The server verifies the client certificate
  doesnt support jks 
  
  https://gist.github.com/mtigas/952344 --> generate a crt and pkcs12 
  
  
  
