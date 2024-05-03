pipeline {
    agent any
 
    stages {
        stage('Get code from GitHub') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/yasmine-trabelsi/stationski.git']]])
            }
        }
        stage('Maven compile') {
            steps {
                sh 'mvn clean compile'
            }
        }
         stage('Test unitaire') { 
            steps {
                sh 'mvn clean test' 
            }
        }
          stage('Maven Build') {
            steps {
                sh 'mvn clean install'
            }
        }}}
