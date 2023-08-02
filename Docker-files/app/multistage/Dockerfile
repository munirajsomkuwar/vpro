FROM openjdk:11 AS BUILD_IMAGE

# Install Git
RUN apt-get update && apt-get install -y git

# Install Maven
RUN apt-get install -y maven

# Clone the repository, checkout 'docker' branch, and build the project
RUN git clone https://github.com/munirajsomkuwar/vpro.git
RUN cd vpro && git checkout docker && mvn install

FROM tomcat:9-jre11

RUN rm -rf /usr/local/tomcat/webapps/*

COPY --from=BUILD_IMAGE vpro/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
