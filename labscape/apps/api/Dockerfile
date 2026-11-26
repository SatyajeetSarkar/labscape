FROM eclipse-temurin:21-jdk AS build

WORKDIR /workspace

# The API packages reviewed content from the repository-level content/ directory.
COPY labscape/apps/api/ apps/api/
COPY labscape/content/ content/

WORKDIR /workspace/apps/api
RUN chmod +x ./mvnw && ./mvnw --batch-mode --no-transfer-progress -DskipTests package

FROM eclipse-temurin:21-jre

WORKDIR /app
COPY --from=build /workspace/apps/api/target/labscape-api-*.jar /app/app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app/app.jar"]
