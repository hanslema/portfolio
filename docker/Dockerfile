FROM khipu/openjdk17-alpine

EXPOSE 8070

ENV APP_HOME /var/lib/jenkins/workspace/Hurt/target

COPY my-project-1.1.1.jar $APP_HOME/app.jar

WORKDIR $APP_HOME

ENTRYPOINT ["java", "-jar", "my-project-1.1.1.jar"]
