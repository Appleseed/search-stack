# Apache Cassandra 3.9 on Nanoserver [ Thin UI Less ]
 
FROM microsoft/nanoserver

SHELL ["powershell"]

MAINTAINER ANANT Corporation https://www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Setup Working Directories
RUN MD C:\\cassandra
    
WORKDIR C:\\cassandra

#Install 7zip
RUN powershell -Command "Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force;Set-PSRepository -Name PSGallery -InstallationPolicy Trusted;Install-Module PS7Zip;"

#Add Open Source Java 1.8
ADD https://github.com/ojdkbuild/ojdkbuild/releases/download/1.8.0.91-3/java-1.8.0-openjdk-1.8.0.91-3.b14.windows.x86_64.zip c:\\Java\\java.1.8.zip

#Install Java 1.8
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'c:\\Java\\java.1.8.zip' -DestinationPath 'c:\\Java'" ;\
    setx /M JAVA_HOME 'C:\\Java\\java-1.8.0-openjdk-1.8.0.91-3.b14.windows.x86_64' ;\
    rm c:\\Java\\java.1.8.zip
     
#ADD Cassandra 3.9
ADD http://apache.mirrors.ionfish.org/cassandra/3.9/apache-cassandra-3.9-bin.tar.gz C:\\cassandra

#Unzip the main archive
RUN  powershell -Command  "Expand-7Zip C:\\cassandra\\apache-cassandra-3.9-bin.tar.gz"

#Cleanup
RUN rm C:\\cassandra\\apache-cassandra-3.9-bin.tar.gz

#7000	Cassandra inter-node cluster communication.
#7001	Cassandra SSL inter-node cluster communication.
#7199	Cassandra JMX monitoring port.
#8888	OpsCenter website. The opscenterd daemon listens on this port for HTTP requests coming directly from the browser.
EXPOSE 7000 7001 7199 8888
 
CMD powershell -Command "c:\\cassandra\\apache-cassandra-3.9\\bin\\cassandra.bat"

 
