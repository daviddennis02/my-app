# my-app -- About
A maven build app

This is a CI/CD project on AWS using AWS DevOps tools 🧰 :  AWS CodeBuild and AWS CodeDeploy to build a java application using maven as build tool. The application is deployed using a specified deployment script.

## BuildSpec file

buildspec.yml file is a collection of build commands and related settings, in YAML format, that CodeBuild uses to run a build. I specify the buildspec.yml file in AWS CodeBuild in order to run the build, which results to a packaged artifact that can be deployed.
```
## Build CI
version: 0.2

phases:
  install:
    runtime-versions:
      java: corretto8
  build:
    commands:
      - echo Build started on `date`
      - mvn test 
  post_build:
    commands:
      - echo Build completed on `date`
      - mvn package
artifacts:
  files:
    - target/my-app-1.0-SNAPSHOT.jar
    - appspec.yml
  discard-paths: yes
```



## AppSpec file

appspec.yml, application specification file (AppSpec file) is a YAML -formatted or JSON-formatted file used by CodeDeploy to manage a deployment.
```
# Deploy file - CD
version: 0.0
os: linux
files:
  - source: ./my-app-1.0-SNAPSHOT.jar
    destination: /tmp
```

## Requirements
* AWS Account

