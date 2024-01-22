FROM khipu/openjdk17-alpine

EXPOSE 8070

ENV APP_HOME /home/hans/Documents/For\Hans/portfolio

COPY target/my-project-1.1.1.jar $APP_HOME/app.jar

WORKDIR $APP_HOME

ENTRYPOINT ["java", "-jar", "my-project-1.1.1.jar"]
