pipeline {
    agent { label 'ltecomm'}
    triggers { cron('H * * * 1-5') }
    stages {
        stage ('scm') {
            steps {
                git branch : 'developer' , url : 'https://github.com/pramesh123/mul0gol.git'
            }

        }
        stage('Build') {
            steps {
                withSonarQubeEnv('SONAR-7.1') {

                sh 'mvn clean package sonar:sonar'
                }
            }
            }

        }

        stage ('post build') {
            steps {
            archiveArtifacts artifacts: 'gameoflife-web/target/gameoflife.war', fingerprint: true
            //stash name: 'warfile', includes: 'gameoflife-web/target/*.war'
        }
        }
        
        
    }
    post {
        always {
            mail to : 'rams.pattipaka@gmail.com',
            subject : "status of pipeline ${currentBuild.fullDisplayName}",
            body: "${env.BUILD_URL} has result ${currentBuild.result}" 
        }
    }


