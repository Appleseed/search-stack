# Appleseed.Search.Base Engine 
 
FROM microsoft/windowsservercore

SHELL ["powershell"]

MAINTAINER ANANT Corporation www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Setup Working Directories
RUN MD C:\\Appleseed\\Search\\Engine
WORKDIR C:\\Appleseed\\Search\\Engine

ADD https://github.com/Appleseed/search/releases/download/latest/IndexService.zip C:\\Appleseed\\Search

#Unzip the main archive
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Appleseed\\Search\\IndexService.zip' -DestinationPath 'c:\\Appleseed\\Search\\Engine'"
    
#Cleanup

RUN rm  C:\\Appleseed\\Search\\IndexService.zip

CMD powershell -Command  ping -t localhost
 
