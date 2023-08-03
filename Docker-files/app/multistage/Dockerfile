# Stage 1: Build the application
FROM openjdk:11 AS BUILD_IMAGE

# Install Git and Maven
RUN apt-get update && apt-get install -y git maven

# Clone the repository, checkout 'docker' branch, and build the project
WORKDIR /app
RUN git clone https://github.com/munirajsomkuwar/vpro.git && \
    cd vpro && \
    git checkout docker && \
    mvn install

# Stage 2: Create the final image
FROM tomcat:9-jre11

# Remove default webapps from Tomcat
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy the built artifact from Stage 1 to the Tomcat webapps directory
COPY --from=BUILD_IMAGE /app/vpro/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

# Expose port 8080 for Tomcat
EXPOSE 8080

# Start Tomcat
CMD ["catalina.sh", "run"]
