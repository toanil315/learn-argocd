## build stage ##
FROM maven:3.8.3-eclipse-temurin-17 AS build

WORKDIR /app
COPY . .

RUN mvn install -DskipTests=true

## run stage ##
FROM eclipse-temurin:17-jdk

# Set time zone (works on Debian-based images)
RUN apt-get update && apt-get install -y tzdata && \
    ln -snf /usr/share/zoneinfo/Asia/Ho_Chi_Minh /etc/localtime && \
    echo "Asia/Ho_Chi_Minh" > /etc/timezone && \
    apt-get clean

COPY --from=build /app/target/spring-boot-ecommerce-0.0.1-SNAPSHOT.jar /run/spring-boot-ecommerce-0.0.1-SNAPSHOT.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/run/spring-boot-ecommerce-0.0.1-SNAPSHOT.jar"]
