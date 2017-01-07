# Elastic 5.1.1 on Nanoserver [ Thin UI Less ]
# TO:DO - Add Env Variables | Add Intial Schema ( perhaps as env var )
 
FROM microsoft/nanoserver

SHELL ["powershell"]

MAINTAINER ANANT Corporation https://www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Setup Working Directories
RUN MD C:\\Tempsoft ;\
    MD C:\\elastic 
    
WORKDIR C:\\elastic

#Install 7zip
RUN powershell -Command "Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force;Set-PSRepository -Name PSGallery -InstallationPolicy Trusted;Install-Module PS7Zip;"

#Add Open Source Java 1.8
ADD https://github.com/ojdkbuild/ojdkbuild/releases/download/1.8.0.91-3/java-1.8.0-openjdk-1.8.0.91-3.b14.windows.x86_64.zip c:\\Java\\java.1.8.zip

#Install Java 1.8
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'c:\\Java\\java.1.8.zip' -DestinationPath 'c:\\Java'" ;\
   setx /M JAVA_HOME 'C:\\Java\\java-1.8.0-openjdk-1.8.0.91-3.b14.windows.x86_64'
     
#ADD Elasticsearch 5.1.1 
ADD https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.1.1.zip C:\\Tempsoft

#Unzip the main archive
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Tempsoft\\elasticsearch-5.1.1.zip' -DestinationPath 'C:\\elastic'"
  
#Cleanup
RUN rm C:\\Tempsoft\\elasticsearch-5.1.1.zip  

EXPOSE 9200 9300
 
CMD powershell -Command "c:\\elastic\\elasticsearch-5.1.1\\bin\\elasticsearch.bat --E network.host=0.0.0.0"

 
