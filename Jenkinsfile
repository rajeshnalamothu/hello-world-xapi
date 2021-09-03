pipeline {

  agent any
  environment {
    ANYPOINT_CREDS = credentials('anypoint.credentials')
    ANYPOINT_URL = "https://anypoint.mulesoft.com"
    MULE_VERSION = "4.3.0"
  }
  stages {
    stage('Build') {
      steps {
      		echo 'Building...'
            bat 'mvn clean -DskipTests package'
      }
    }

    stage('Test') {
      steps {
         echo 'Skipping Tests...'
         //bat "mvn test"
      }
    }

     stage('Deploy Design') {
      environment {
        ENVIRONMENT = 'Design'
        APP_NAME = 'hello-world-sapi-dev'
        WORKERS = '1'
        WORKER_TYPE = 'MICRO'
      }
      steps {
      		echo 'Deploying to Design Environment...'
            bat 'mvn -DskipTests -PDesign deploy -DmuleDeploy -Danypoint.url="%ANYPOINT_URL%" -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.application.name="%APP_NAME%" -Denvironment="%ENVIRONMENT%" -Dworkers="%WORKER%"' -DworkerType="%WORKER_TYPE%"'
      }
    }
    stage('Deploy Sandbox') {
      environment {
        ENVIRONMENT = 'Sandbox'
        APP_NAME = 'hello-world-sapi-test'
        WORKERS = '1'
        WORKER_TYPE = 'MICRO'
      }
      steps {
      		echo 'Deploying to Sandbox Environment...'
            bat 'mvn -DskipTests -PSandbox deploy -DmuleDeploy -Danypoint.url="%ANYPOINT_URL%" -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.application.name="%APP_NAME%" -Denvironment="%ENVIRONMENT%" -Dworkers="%WORKER%"' -DworkerType="%WORKER_TYPE%"'
      }
    }
  }
}