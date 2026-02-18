FROM maven:3.9.9-eclipse-temurin-21 AS builder

WORKDIR /app

COPY pom.xml .

RUN --mount=type=cache,target=/root/.m2 \
    mvn dependency:resolve -B

COPY src ./src

# Build only patient-service
RUN --mount=type=cache,target=/root/.m2 \
    mvn clean package -DskipTests -B -T 1C

FROM eclipse-temurin:21-jdk AS runner
WORKDIR /app

COPY --from=builder ./app/target/analytics-service-0.0.1-SNAPSHOT.jar ./app.jar

EXPOSE 4002

ENTRYPOINT ["java","-jar","app.jar"]
