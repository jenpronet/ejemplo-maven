import groovy.json.JsonSlurperClassic
def jsonParse(def json) {
    new groovy.json.JsonSlurperClassic().parseText(json)
}
pipeline {
    agent any
    stages {
        stage("Paso 0: Instalar Maven"){
            steps {
               script {
                   //Puede que falle por permisos
                sh "apt-get update&& apt-get install -y  maven"
                }
            }
        }
        stage("Paso 1: Download and checkout"){
            steps {
               checkout(
                        [$class: 'GitSCM',
                        branches: [[name: "jenkins-pipeline-as-code" ]],
                        userRemoteConfigs: [[url: 'https://github.com/intohybrid/ejemplo-maven']]])
            }
        }
        stage("Paso 2: Compliar"){
            steps {
                script {
                sh "echo 'Compile Code!'"
                // Run Maven on a Unix agent.
                sh "mvn clean compile -e"
                }
            }
        }
        stage("Paso 3: Testear"){
            steps {
                script {
                sh "echo 'Test Code!'"
                // Run Maven on a Unix agent.
                sh "mvn clean test -e"
                }
            }
        }
        stage("Paso 4: Build .Jar"){
            steps {
                script {
                sh "echo 'Build .Jar!'"
                // Run Maven on a Unix agent.
                sh "mvn clean package -e"
                }
            }
        }
    }
    post {
        always {
            sh "echo 'fase always executed post'"
        }
        success {
            sh "echo 'fase success'"
        }
        failure {
            sh "echo 'fase failure'"
        }
    }
}