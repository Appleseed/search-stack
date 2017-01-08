# MongoDB 3.4.1 on Nanoserver [ Thin UI Less ]

FROM microsoft/nanoserver

SHELL ["powershell"]

MAINTAINER ANANT Corporation https://www.anant.us | Report Issues : https://github.com/Appleseed/search-stack/issues

#Setup Working Directories
RUN MD C:\\MongoDB ;\
    MD C:\\MongoDB\\data\\db
    
WORKDIR C:\\MongoDB

#Install 7zip
RUN powershell -Command "Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force;Set-PSRepository -Name PSGallery -InstallationPolicy Trusted;Install-Module PS7Zip;"

#Add Open Source Java 1.8
#Install Java 1.8
#RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'c:\\Java\\java.1.8.zip' -DestinationPath 'c:\\Java'" ;\
#   setx /M JAVA_HOME 'C:\\Java\\java-1.8.0-openjdk-1.8.0.91-3.b14.windows.x86_64'
     
#ADD Mongo 3.4.1
ADD http://downloads.mongodb.org/win32/mongodb-win32-x86_64-2008plus-ssl-v3.4-latest.zip?_ga=1.111665540.1262978244.1483896705 c:\\MongoDB\\Mongo.zip

#Unzip the main archive
RUN  powershell -Command  "Expand-7Zip C:\\MongoDB\\Mongo.zip" ;\
     Rename-Item mongodb-win32-x86_64-2008plus-ssl-3.4.1-62-gb758d56 3.4.1
  
#Cleanup
RUN rm C:\\MongoDB\\Mongo.zip  

#The default port for mongod and mongos instances is 27017
EXPOSE 27017 27018 27019
 
#CMD powershell -Command "c:\\MongoDB\\3.4.1\\bin\\mongod.exe"
CMD powershell -Command  ping -t localhost

 
