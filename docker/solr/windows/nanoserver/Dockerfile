# Solr 5.5.3 on Windows Nano Server 2016 ( Thin UI Less)
 
FROM microsoft/nanoserver

SHELL ["powershell"]

MAINTAINER ANANT Corporation www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Setup Working Directories
RUN MD C:\\solr 
 
WORKDIR C:\\solr

RUN powershell -Command "Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force;Set-PSRepository -Name PSGallery -InstallationPolicy Trusted;Install-Module PS7Zip;"

ADD https://github.com/ojdkbuild/ojdkbuild/releases/download/1.8.0.91-3/java-1.8.0-openjdk-1.8.0.91-3.b14.windows.x86_64.zip c:\\Java\\java.1.8.zip

RUN powershell -Command "Expand-7Zip c:\\Java\\java.1.8.zip" ;\
   setx /M JAVA_HOME 'C:\\Java\\Java.1.8'
  
#Pull down Proxy
#ADD https://github.com/Appleseed/portal-stack/releases/download/v1.2.0.0/solr.proxy.config.zip C:\\Appleseed\\Proxy    
    
#RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Appleseed\\Proxy\\solr.proxy.config.zip' -DestinationPath ' C:\\Appleseed\\Proxy'" ;\
#    rm C:\\Appleseed\\Proxy\\solr.proxy.config.zip

    
 # ADD Solr 5.5.3
ADD http://apache.mirrors.ionfish.org/lucene/solr/5.5.3/solr-5.5.3.zip  C:\\solr
#Unzip the main archive
#Solr is so large it needs 7zip to unzip and not error
RUN  powershell -Command  "Expand-7Zip C:\\solr\\solr-5.5.3.zip"
  

#Cleanup
RUN rm  C:\\solr\\solr-5.5.3.zip  

#Add Core | Start Solr
ADD https://github.com/Appleseed/portal-stack/releases/download/v1.2.0.0/appleseed-search.core.zip C:\\solr
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\solr\\appleseed-search.core.zip' -DestinationPath 'c:\\solr\\solr-5.5.3\\example'" ;\
    rm C:\\solr\\appleseed-search.core.zip 
   
EXPOSE 8983 

CMD powershell -Command  "c:\\solr\\solr-5.5.3\\bin\\solr.cmd start -p 8983 -f -s c:\\solr\\solr-5.5.3\\example\\appleseed-search\\solr -V"


 
