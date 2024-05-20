pipeline {
    agent any
    stages {
        stage('Package') { 
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('Building image') {
            steps {
                bat 'docker build -t teedy-image .'
            }
        }
        stage('upload image') {
            steps {
                    bat 'docker login -u dragon12112528 -p AaLOL123456'
                    bat 'docker tag teedy-image dragon12112528/teedy:teedy-image'
                    bat 'docker push dragon12112528/teedy:teedy-image'
                }
            }
        stage('run container') {
            steps {
                bat 'docker run -d -p 8081:8080 --name teedy-container1 dragon12112528/teedy:teedy-image'
                bat 'docker run -d -p 8082:8080 --name teedy-container2 dragon12112528/teedy:teedy-image'
                bat 'docker run -d -p 8083:8080 --name teedy-container3 dragon12112528/teedy:teedy-image'
            }
        }
    }
}