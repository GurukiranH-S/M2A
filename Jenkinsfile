pipeline {
agent any
tools {
    maven 'Maven'
}

stages {

    stage('Checkout') {
        steps {
            git branch: 'main',
                url: 'https://github.com/GurukiranH-S/M2A.git'
        }
    }

    stage('Build') {
        steps {
            sh 'mvn clean package'
        }
    }

    

    stage('Test') {
        steps {
            sh 'mvn test'
        }
    }


    stage('Run Application') {
        steps {
            sh 'nohup java -jar target/M2A-1.0-SNAPSHOT.jar'
        }
    }
}

post {
    success {
        echo 'Build, Test, and Packaging completed successfully!'
    }

    failure {
        echo 'Build failed. Check console logs.'
    }

    always {
        cleanWs()
    }
}

}
