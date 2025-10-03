FROM openjdk:11 AS BUILD_IMAGE

RUN apt-get update && apt-get install -y maven

COPY . /app
WORKDIR /app
RUN mvn clean package -DskipTests

FROM tomcat:9-jre11

RUN rm -rf /usr/local/tomcat/webapps/*

# ✅ Correct WAR path
COPY --from=BUILD_IMAGE /app/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
