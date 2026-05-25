FROM maven:3.9.9-eclipse-temurin-21-jammy AS build
RUN git clone https://github.com/hkhcoder/vprofile-project.git
WORKDIR /vprofile-project
RUN git checkout containers && mvn install

FROM tomcat:10-jdk21
LABEL project="vprofile-project"
LABEL Author="Tushar"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=build /vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh","run"]