FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && apt install maven -y
RUN git clone https://github.com/ChandulaJ/vprofile-project-d.git
RUN cd vprofile-project-d && git checkout docker && mvn install

FROM tomcat:9-jre11
LABEL "Project"="vprofile"
LABEL "Author"="Chandula Jayathilake"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE /vprofile-project-d/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]