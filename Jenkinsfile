pipeline {
agent any
tools {
    maven 'Maven'
}

stages {

    stage('Checkout') {
        steps {
            git branch: 'main',
                url: 'https://github.com/Gurukiran-H-S/myMavenApp.git'
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

    stage('Archive Artifact') {
        steps {
            archiveArtifacts artifacts: 'target/*.jar',
                             fingerprint: true
        }
    }

    stage('Run Application') {
        steps {
            sh 'nohup java -jar target/M2A-1.0-SNAPSHOT.jar > app.log 2>&1 &'
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
```

}
