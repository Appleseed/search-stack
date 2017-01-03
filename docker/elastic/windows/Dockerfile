# Elastic 2.4.3 /  5.1.1 on Windows Server Core 2016 ( UI Less)
# TO:DO - Add Env Variables 
 
FROM microsoft/windowsservercore

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
    choco install iis-arr ;\
    choco install git ;\
    choco install nodejs
    
#Pull down Proxy
ADD https://github.com/Appleseed/portal-stack/releases/download/v1.2.0.0/elastic.proxy.config.zip C:\\Appleseed\\Proxy    
    
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Appleseed\\Proxy\\elastic.proxy.config.zip' -DestinationPath ' C:\\Appleseed\\Proxy'" ;\
    rm C:\\Appleseed\\Proxy\\elastic.proxy.config.zip

#Create an IIS Proxy
RUN Remove-WebSite -Name 'Default Web Site'  ;\
    New-Website -Name 'Appleseed.Search.Proxy' -Port 80 \  
    -PhysicalPath 'c:\Appleseed\Proxy' -ApplicationPool '.NET v4.5'
 
# ADD Elastic 2.4.3 for ItemsAPI | Leave 5.1.1 link for future / Add to env variables
#ADD https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.1.1.zip C:\\Tempsoft
ADD https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/zip/elasticsearch/2.4.3/elasticsearch-2.4.3.zip  C:\\Tempsoft

#Unzip the main archive
#RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Tempsoft\\elasticsearch-5.1.1.zip' -DestinationPath 'C:\\elastic'"
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Tempsoft\\elasticsearch-2.4.3.zip' -DestinationPath 'C:\\elastic'"
  
#Cleanup
#RUN rm C:\\Tempsoft\\elasticsearch-5.1.1.zip  
RUN rm C:\\Tempsoft\\elasticsearch-2.4.3.zip

#EXPOSE 80 9200
EXPOSE 9200 9300
 
#CMD powershell -Command "c:\\elastic\\elasticsearch-5.1.1\\bin\\elasticsearch.bat"
CMD powershell -Command "c:\\elastic\\elasticsearch-2.4.3\\bin\\elasticsearch.bat --Des.network.host=0.0.0.0"

 
