pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'nouvelle-branche', url: 'https://github.com/ahmedsallemi34/DS2.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Analyse SonarQube') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                        mvn sonar:sonar \
                        -Dsonar.projectKey=demo \
                        -Dsonar.host.url=http://192.168.50.4:9000
                    '''
                }
            }
        }
        stage('Construire Image Docker') {
            steps {
                
                sh 'docker build -t ahmedsallemi34/school:latest .'
            }
        }
    }
}
