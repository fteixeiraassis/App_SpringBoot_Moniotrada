# FROM openjdk:8-jdk-alpine
# RUN addgroup -S spring && adduser -S spring -G spring
# USER spring:spring
# ARG JAR_FILE=target/*jar
# COPY ${JAR_FILE} app.jar
# ENTRYPOINT ["java","-Xms128M","-Xmx128M","-XX:PermSize=64m","-XX:MaxPermSize=128m","-Dspring.profiles.active=prod","-jar","/app.jar"]

#build da aplicação
FROM maven:3-jdk-11 as builder
WORKDIR /app
COPY . .
RUN mvn clean package
#ARG JAR_FILE=./target/forum.jar

FROM openjdk:8-jdk-alpine
#WORKDIR /app
COPY --from=builder /app/target/*jar ./app.jar
RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring
# ARG JAR_FILE
# RUN echo ${JAR_FILE}
# COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-Xms128M","-Xmx128M","-XX:PermSize=64m","-XX:MaxPermSize=128m","-Dspring.profiles.active=prod","-jar","/app.jar"]