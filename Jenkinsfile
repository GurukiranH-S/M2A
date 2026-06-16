pipeline {
agent any

tools {
    maven 'Maven'
    jdk 'JDK17'
}

stages {

    stage('Checkout') {
        steps {
            git branch: 'main',
                url: 'https://github.com/GurukiranH-S/M2A.git'
        }
    }

    stage('Clean') {
        steps {
            sh 'mvn clean'
        }
    }

    stage('Compile') {
        steps {
            sh 'mvn compile'
        }
    }

    stage('Test') {
        steps {
            sh 'mvn test'
        }
        post {
            always {
                junit 'target/surefire-reports/*.xml'
            }
        }
    }

    stage('Package') {
        steps {
            sh 'mvn package'
        }
    }

    stage('Show Artifact') {
        steps {
            sh 'ls -lh target/'
        }
    }

    stage('Run Application') {
        steps {
            sh '''
                echo "===== APPLICATION OUTPUT ====="
                java -jar target/M2A-1.0-SNAPSHOT.jar
                echo "===== APPLICATION COMPLETED ====="
            '''
        }
    }
}

post {
    success {
        echo 'Build, Test and Run Successful!'
    }

    failure {
        echo 'Build Failed!'
    }

    always {
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
    }
}

}
