# proj
[![Build Status](https://travis-ci.org/julesbond007/proj.svg?branch=master)](https://travis-ci.org/julesbond007/proj)
[![Coverage Status](https://coveralls.io/repos/github/julesbond007/proj/badge.svg?branch=master)](https://coveralls.io/github/julesbond007/proj?branch=master)

Scheduled service to fetch events from github and publish them to slack using producer/consumer pattern.  If an event fails to process, the application will send an email notification.

#Running
0. Update [config.properties](https://github.com/julesbond007/event-scheduler/blob/master/project-service/src/main/resources/config.properties) to have correct slack token/channel & github login/password (optional for rate control)
1. To build the project:
  <p>if gradle is installed do `gradle clean build`</p>
  <p>otherwise `chmod +x gradlew` then `./gradlew clean build`</p>
2. Deploy the project to tomcat or other server: 
  <p>`cp -r project-api/build/libs/project-api-1.0.war $TOMCAT_HOME/webapps/proj.war`</p>
3. Start the scheduler (delay and frequency are in minutes): 
  <p>`POST http://localhost:8080/proj/api/v1/scheduler/actions/start` request body: `{"delay":1, "frequency":5}`</p>
4. Stop the scheduler: 
  <p>`POST http://localhost:8080/proj/api/v1/scheduler/actions/stop`</p>