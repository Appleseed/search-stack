# Elastic 2.4.3 |  5.1.1 w/ ItemsAPI on Windows Server Core 2016 ( UI Less)
# TO:DO - Add Env Variables 
 
FROM microsoft/windowsservercore

SHELL ["powershell"]

MAINTAINER ANANT Corporation www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Setup Working Directories
RUN MD C:\\Tempsoft ;\
    MD C:\\elastic ;\
    MD C:\\ItemsAPI
    
WORKDIR C:\\elastic


#Install chocolatey
RUN $env:chocolateyUseWindowsCompression = 'false' ;\
    iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1')) ;\
    chocolatey feature enable -n=allowGlobalConfirmation ;\
    choco install jdk8 ;\
    choco install 7zip.install ;\
    choco install git ;\
    choco install nodejs
    
 
# ADD Elastic 2.4.3 for ItemsAPI | Leave 5.1.1 link for future / Add to env variables
#ADD https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.1.1.zip C:\\Tempsoft
ADD https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/zip/elasticsearch/2.4.3/elasticsearch-2.4.3.zip  C:\\Tempsoft

#Unzip the main archive
#RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Tempsoft\\elasticsearch-5.1.1.zip' -DestinationPath 'C:\\elastic'"
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Tempsoft\\elasticsearch-2.4.3.zip' -DestinationPath 'C:\\elastic'"
  
#Cleanup
#RUN rm C:\\Tempsoft\\elasticsearch-5.1.1.zip  
RUN rm C:\\Tempsoft\\elasticsearch-2.4.3.zip

#Install ItemsAPI
RUN cd C:\\ItemsAPI ;\
    git clone https://github.com/itemsapi/itemsapi.git 
   # To-Do discover how to call install and continue step | Currently it pauses the step and works better during a container run
   # npm install

#EXPOSE 80 9200
EXPOSE 9200 9300 3000
 
#CMD powershell -Command "c:\\elastic\\elasticsearch-5.1.1\\bin\\elasticsearch.bat"
CMD powershell -Command "c:\\elastic\\elasticsearch-2.4.3\\bin\\elasticsearch.bat --Des.network.host=0.0.0.0"

 
