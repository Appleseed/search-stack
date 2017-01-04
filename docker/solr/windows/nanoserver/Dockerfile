# Solr 5.5.3 on Windows Nano Server 2016 ( Thin UI Less)
 
FROM microsoft/nanoserver

SHELL ["powershell"]

MAINTAINER ANANT Corporation www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Setup Working Directories
RUN MD C:\\solr ;\
    MD C:\\Tempsoft  
       
WORKDIR C:\\solr

RUN powershell -Command "Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force;Set-PSRepository -Name PSGallery -InstallationPolicy Trusted;Install-Module PS7Zip;"

ADD https://github.com/ojdkbuild/ojdkbuild/releases/download/1.8.0.91-3/java-1.8.0-openjdk-1.8.0.91-3.b14.windows.x86_64.zip java.zip

RUN powershell -Command "Expand-7Zip java.zip" ;\
     $env:JAVA_HOME=C:\\java-1.8.0-openjdk-1.8.0.91-3.b14.windows.x86_64
  
#Pull down Proxy
ADD https://github.com/Appleseed/portal-stack/releases/download/v1.2.0.0/solr.proxy.config.zip C:\\Appleseed\\Proxy    
    
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Appleseed\\Proxy\\solr.proxy.config.zip' -DestinationPath ' C:\\Appleseed\\Proxy'" ;\
    rm C:\\Appleseed\\Proxy\\solr.proxy.config.zip

    
 # ADD Solr 5.5.3
ADD http://apache.mirrors.ionfish.org/lucene/solr/5.5.3/solr-5.5.3.zip  C:\\Tempsoft
#Unzip the main archive
#Solr is so large it needs 7zip to unzip and not error
RUN  cd c:\\Tempsoft ;\
     powershell -Command  "Expand-7Zip C:\\Tempsoft\\solr-5.5.3.zip c:\\solr"
  

#Cleanup
RUN rm  C:\\Tempsoft\\solr-5.5.3.zip  

#Add Core | Start Solr
ADD https://github.com/Appleseed/portal-stack/releases/download/v1.2.0.0/appleseed-search.core.zip C:\\Tempsoft
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Tempsoft\\appleseed-search.core.zip' -DestinationPath 'c:\\solr\\solr-5.5.3\\example'" ;\
    rm C:\\Tempsoft\\appleseed-search.core.zip 
   
EXPOSE 8983 

CMD powershell -Command  "c:\\solr\\solr-5.5.3\\bin\\solr.cmd start -p 8983 -f -s c:\\solr\\solr-5.5.3\\example\\appleseed-search\\solr -V"


 
