# Solr 6.4.1 (Latest) on Windows Nanoserver 2016 [Tiny Image | No UI]
 
FROM microsoft/nanoserver

SHELL ["powershell"]

MAINTAINER ANANT Corporation https://www.anant.us | Report Issues : https://github.com/Appleseed/search-stack/issues

#Setup Working Directories
RUN MD C:\\solr 
 
WORKDIR C:\\solr

RUN powershell -Command "Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force;Set-PSRepository -Name PSGallery -InstallationPolicy Trusted;Install-Module PS7Zip;"

ADD https://github.com/ojdkbuild/ojdkbuild/releases/download/1.8.0.91-3/java-1.8.0-openjdk-1.8.0.91-3.b14.windows.x86_64.zip c:\\Java\\java.1.8.zip

RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'c:\\Java\\java.1.8.zip' -DestinationPath 'c:\\Java'" ;\
   setx /M JAVA_HOME 'C:\\Java\\java-1.8.0-openjdk-1.8.0.91-3.b14.windows.x86_64' 
  
# ADD Solr 6.4.1
ADD http://apache.claz.org/lucene/solr/6.4.1/solr-6.4.1.zip C:\\solr
#Unzip the main archive
#Solr is so large it needs 7zip to unzip and not error
RUN  powershell -Command  "Expand-7Zip C:\\solr\\solr-6.4.1.zip"
  
#Cleanup
RUN rm  C:\\solr\\solr-6.4.1.zip  

#Add Core | Copy Required Example files for Core to start
ADD https://github.com/Appleseed/portal-stack/releases/download/v1.2.0.0/appleseed-search.core.zip C:\\solr
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\solr\\appleseed-search.core.zip' -DestinationPath 'c:\\solr\\solr-6.4.0\\example'" ;\
    rm C:\\solr\\appleseed-search.core.zip ;\
    cp c:\\solr\\solr-6.4.0\\example\\example-DIH\\solr\\solr\\conf\\xslt c:\\solr\\solr-6.4.0\\example\\appleseed-search\\solr\\appleseed-public\\conf ;\
    cp c:\\solr\\solr-6.4.0\\example\\example-DIH\\solr\\solr\\conf\\clustering c:\\solr\\solr-6.4.0\\example\\appleseed-search\\solr\\appleseed-public\\conf ;\
    cp c:\\solr\\solr-6.4.0\\example\\example-DIH\\solr\\solr\\conf\\lang\\stopwords_ckb.txt c:\\solr\\solr-6.4.0\\example\\appleseed-search\\solr\\appleseed-public\\conf\\lang ;\
    cp c:\\solr\\solr-6.4.0\\example\\example-DIH\\solr\\solr\\conf\\solrconfig.xml c:\\solr\\solr-6.4.0\\example\\appleseed-search\\solr\\appleseed-public\\conf

COPY conf/managed-schema c:/solr/solr-6.4.0/example/appleseed-search/solr/appleseed-public/conf

EXPOSE 8983 

#Turn Solr to startup when the container starts
CMD powershell -Command  "c:\\solr\\solr-6.4.0\\bin\\solr.cmd start -p 8983 -f -s c:\\solr\\solr-6.4.0\\example\\appleseed-search\\solr -V"


 
