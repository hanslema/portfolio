FROM adoptopenjdk:17-jdk-hotspot-boinic

EXPOSE 8070

ENV APP_HOME /home/hans/Documents/For Hans/Hans.com/portfolio

COPY portfolio-0.0.1-SNAPSHOT.jar $APP_HOME/app.jar

WORKDIR $APP_HOME

ENTRYPOINT ["java", "-jar", "portfolio-0.0.1-SNAPSHOT.jar"]
