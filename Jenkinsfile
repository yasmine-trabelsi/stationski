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
        }
          stage("SonarQube Analysis") {
            steps {
                script {
                 def scannerHome = tool 'scanner'
                 withSonarQubeEnv(installationName: 'stationski'){
                   sh 'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=sonar'
                 }
                }
            }
        }
          stage('Building Image') {
            steps {
                sh 'docker build -t yasmine425/stationski .'
            }
        }
        stage('Push Image to DockerHub') {
            steps {
                script {
                    sh("docker login -u 'yasmine425' -p admin1234 ")
                    sh('docker push yasmine425/stationski')
                }
            }

    }}}
