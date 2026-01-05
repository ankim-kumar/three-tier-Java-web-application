FROM maven:3.9.9-eclipse-temurin-21-jammy AS build

WORKDIR /app

# Copy only pom.xml first (layer caching)
COPY pom.xml .
RUN mvn dependency:go-offline

# Copy only application source
COPY src ./src

# Build WAR
RUN mvn clean package -DskipTests

FROM tomcat:10.1-jdk21

RUN rm -rf /usr/local/tomcat/webapps/*

COPY --from=build /app/target/vprofile-v2.war \
  /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
