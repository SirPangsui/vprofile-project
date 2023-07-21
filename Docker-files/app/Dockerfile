# Stage 1: Build the Java application using Maven
FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && apt install maven -y
RUN git clone https://github.com/devopshydclub/vprofile-project.git
RUN cd vprofile-project && git checkout docker && mvn install

# Stage 2: Deploy the application using Tomcat 9
FROM tomcat:9-jre11
LABEL "Project"="Vprofile"
LABEL "Author"="SirPangsui"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE /vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]


