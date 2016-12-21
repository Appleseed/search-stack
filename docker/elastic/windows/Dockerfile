# Elastic 5.1.1 on Windows Server Core 2016 ( UI Less)
 
FROM microsoft/iis

SHELL ["powershell"]

MAINTAINER ANANT Corporation www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Setup Working Directories
RUN MD C:\\Tempsoft ;\
    MD C:\\elastic ;\
    MD C:\\Appleseed\\Proxy
    
WORKDIR C:\\elastic

#Install .NET 4.6.1 / IIS Management Tools
RUN Install-WindowsFeature NET-Framework-45-ASPNET ; \  
    Install-WindowsFeature Web-Asp-Net45 ;\
    Install-WindowsFeature Web-Scripting-Tools ;\
    Install-WindowsFeature Web-Static-Content

#Install chocolatey
RUN $env:chocolateyUseWindowsCompression = 'false' ;\
    iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1')) ;\
    chocolatey feature enable -n=allowGlobalConfirmation ;\
    choco install jdk8 ;\
    choco install 7zip.install ;\
    choco install urlrewrite ;\
    choco install nssm ;\
    choco install iis-arr
    
#Pull down Proxy
ADD https://github.com/Appleseed/portal-stack/releases/download/v1.1.1.0/elastic.proxy.config.zip C:\\Appleseed\\Proxy    
    
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Appleseed\\Proxy\\elastic.proxy.config.zip' -DestinationPath ' C:\\Appleseed\\Proxy'" ;\
    rm C:\\Appleseed\\Proxy\\elastic.proxy.config.zip

#Create an IIS Proxy
RUN Remove-WebSite -Name 'Default Web Site'  ;\
    New-Website -Name 'Appleseed.Search.Proxy' -Port 80 \  
    -PhysicalPath 'c:\Appleseed\Proxy' -ApplicationPool '.NET v4.5'
 
# ADD Elastic 5.1.1
ADD https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.1.1.zip C:\\Tempsoft

#Unzip the main archive
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Tempsoft\\elasticsearch-5.1.1.zip' -DestinationPath 'C:\\elastic'"
 
#Cleanup
RUN rm C:\\Tempsoft\\elasticsearch-5.1.1.zip  

#Start Elastic
#RUN c:\\elastic\\elasticsearch-5.1.1\\bin\\elasticsearch.bat

EXPOSE 80

#ENTRYPOINT ["c:\\elastic\\elasticsearch-5.1.1\\bin\\elasticsearch.bat"]
#RUN c:\\elastic\\elasticsearch-5.1.1\\bin\\elasticsearch.bat

#Add Solr As a Service
RUN $params = @('install', 'ElasticSearch', 'c:\\elastic\\elasticsearch-5.1.1\\bin\\elasticsearch.bat', \
           'c:\\elastic\\elasticsearch-5.1.1\\bin', '') ;\
    nssm $params
    
RUN Start-Service ElasticSearch
 
