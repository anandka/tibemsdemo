FROM java:8 

# Install maven
RUN apt-get update  
RUN apt-get install -y maven

WORKDIR /code

# Prepare by downloading dependencies
ADD pom.xml /code/pom.xml  
WORKDIR /code
#RUN ["mvn", "dependency:resolve"]  
#RUN ["mvn", "verify"]

# Adding source, compile and package into a fat jar
ADD src /code/src  
ADD jars /code/jars
WORKDIR /code
RUN ["mvn", "package"]

CMD ["/usr/lib/jvm/java-8-openjdk-amd64/bin/java", "-jar", "target/tibEmsReciever-jar-with-dependencies.jar"] 
