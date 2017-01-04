# Solr 5.5.3 on Windows Nano Server 2016 ( Thin UI Less)
 
FROM microsoft/nanoserver

SHELL ["powershell"]

MAINTAINER ANANT Corporation www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Setup Working Directories
RUN MD C:\\solr ;\
    MD C:\\Tempsoft  
       
WORKDIR C:\\solr

#Install chocolatey and any required tools
RUN $env:chocolateyUseWindowsCompression = 'false' ;\
    iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1')) ;\
    chocolatey feature enable -n=allowGlobalConfirmation ;\
    choco install jdk8 ;\
    choco install 7zip.install ;\
    choco install nssm
  
#Pull down Proxy
ADD https://github.com/Appleseed/portal-stack/releases/download/v1.2.0.0/solr.proxy.config.zip C:\\Appleseed\\Proxy    
    
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Appleseed\\Proxy\\solr.proxy.config.zip' -DestinationPath ' C:\\Appleseed\\Proxy'" ;\
    rm C:\\Appleseed\\Proxy\\solr.proxy.config.zip

    
 # ADD Solr 5.5.3
ADD http://apache.mirrors.ionfish.org/lucene/solr/5.5.3/solr-5.5.3.zip  C:\\Tempsoft
#Unzip the main archive
#Solr is so large it needs 7zip to unzip and not error
RUN cd $env:programfiles\\7-Zip\\ ;\
   ./7z x  C:\\Tempsoft\\solr-5.5.3.zip -oc:\\solr

#Cleanup
RUN rm  C:\\Tempsoft\\solr-5.5.3.zip  

#Add Core | Start Solr
ADD https://github.com/Appleseed/portal-stack/releases/download/v1.2.0.0/appleseed-search.core.zip C:\\Tempsoft
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Tempsoft\\appleseed-search.core.zip' -DestinationPath 'c:\\solr\\solr-5.5.3\\example'" ;\
    rm C:\\Tempsoft\\appleseed-search.core.zip 
   
EXPOSE 8983 

CMD powershell -Command  "c:\\solr\\solr-5.5.3\\bin\\solr.cmd start -p 8983 -f -s c:\\solr\\solr-5.5.3\\example\\appleseed-search\\solr -V"


 
