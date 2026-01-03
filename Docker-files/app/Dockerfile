# ---------- BUILD STAGE ----------
FROM maven:3.9.9-eclipse-temurin-21-jammy AS build

WORKDIR /app

# Copy source code from GitHub Actions workspace
COPY . .

# Build WAR
RUN mvn clean package -DskipTests

# ---------- RUNTIME STAGE ----------
FROM tomcat:10.1-jdk21

RUN rm -rf /usr/local/tomcat/webapps/*

COPY --from=build /app/target/vprofile-v2.war \
     /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080

CMD ["catalina.sh", "run"]
