pipeline {
    agent any
    environment{
        MSG = "HELLO FROM ENVIRONMENT"
    }
    stages {
        stage('Git'){
            steps {
                git url: 'https://github.com/jabedhasan21/java-hello-world-with-maven.git'
                sh 'java -version'
            }
        }
        stage ('Compile'){
          steps {
              echo "${MSG}"
          }
        }
    }
    post{
        always {
             echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
