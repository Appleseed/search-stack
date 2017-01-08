# MSOpenTech Redis 3.2 On Windows Nanoserver : https://github.com/MSOpenTech/redis [ Thin UI Less ]

FROM microsoft/nanoserver

SHELL ["powershell"]

MAINTAINER ANANT Corporation https://www.anant.us | Report Issues : https://github.com/Appleseed/search-stack/issues

#Setup Working Directories
RUN MD C:\\redis
    
WORKDIR C:\\redis

#Install 7zip
#RUN powershell -Command "Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force;Set-PSRepository -Name PSGallery -InstallationPolicy Trusted;Install-Module PS7Zip;"
     
#ADD Redis 3.2 on Windows 
ADD https://github.com/MSOpenTech/redis/releases/download/win-3.2.100/Redis-x64-3.2.100.zip C:\\redis

#Unzip the main archive
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\redis\\Redis-x64-3.2.100.zip' -DestinationPath 'C:\\redis'" 

#Cleanup
RUN rm C:\\redis\\Redis-x64-3.2.100.zip

EXPOSE 6379
 
#CMD powershell -Command "c:\\redis\\redis-win-3.2.100\\redis-server.exe"
CMD powershell -Command  ping -t localhost

