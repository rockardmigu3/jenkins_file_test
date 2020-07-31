pipeline {
   agent any
    environment{
        name = "app-test"
    }
   stages {
      stage('git') {
         steps {
            // Get some code from a GitHub repository
            git 'https://github.com/rockardmigu3/docker_jenkins.git'
            sh 'ls -a'
         }
      }
      stage('build spring'){
          steps{
              sh 'mvn clean install -e'
          }
      }
      stage('run tests'){
            steps{
                sh 'mvn surefire:test test'
            }
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml'
                }
            }
      }
      stage('run sonar'){
          steps{
              withSonarQubeEnv('sonar-jenkins-server') {
                sh 'mvn clean package sonar:sonar'
              }
          }
      }
      stage('build docker file'){
          steps {
            sh 'docker build -t ${name}:${version} .'
          }
      }
      stage('running docker service'){
          steps{
              sh 'docker run -dit --name teste_container -p 9090:9090 ${name}:${version}'
          }
      }
      stage('just an ansible test'){
          steps{
              sh 'ansible 127.0.0.1 -m ping'
          }
      }
   }
}
