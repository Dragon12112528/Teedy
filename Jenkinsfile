pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test -pl core'
            }
        }
        stage('Generate Javadoc') {
            steps {
                sh 'mvn javadoc:javadoc -Dmaven.javadoc.failOnError=false'
            }
        }
        stage('PMD') {
            steps {
                sh 'mvn pmd:pmd -Dformat=html'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/site/apidocs/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/site/pmd.html', fingerprint: true
            archiveArtifacts artifacts: '**/target/surefire-reports/*.xml', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
        }
    }
}