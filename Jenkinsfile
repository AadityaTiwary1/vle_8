pipeline {
    agent any

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/AadityaTiwary1/vle_8.git'
            }
        }

        stage('Apply ConfigMaps') {
            steps {
                sh '''
                kubectl apply -f blue-config.yaml
                kubectl apply -f green-config.yaml
                '''
            }
        }

        stage('Deploy Green') {
            steps {
                sh '''
                kubectl apply -f green.yaml
                '''
            }
        }

        stage('Switch Traffic') {
            steps {
                sh '''
                kubectl patch service my-service -p '{"spec":{"selector":{"app":"myapp","version":"green"}}}'
                '''
            }
        }
    }
}
