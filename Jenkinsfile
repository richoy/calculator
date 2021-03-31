pipeline {
    agent any
    stages {
        stage("Compile") {
            steps {
                sh "./gradlew compileJava"
            }
        }
        stage("Unit Test") {
            steps {
                sh "./gradlew test"
            }
        }
        stage("Code coverage") {
            steps {
                sh "./gradlew jacocoTestReport"
                publishHTML (target: [
                    reportDir: 'build/reports/jacoco/test/html',
                    reportFiles: 'index.html',
                    reportName: "JaCoCo Report"
                ])
                sh "./gradlew jacocoTestCoverageVerification"
            }
        }
        stage("Code Quality") {
            steps{
                sh "./gradlew sonarqube \
                      -Dsonar.projectKey=calculator \
                      -Dsonar.host.url=http://172.17.0.3:9000 \
                      -Dsonar.login=f4b2ea02a17c38ea29904878c5fb1b4655ef6e02"
            }
        }
    }
}