# SSL-Guide
Basic Tutorial that teaches you how to set up a secure SSL with Liberty



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
  
  
  
