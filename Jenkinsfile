pipeline {
    agent any
    
    stages {
        stage("build"){
            steps {
                sh "./mvnw package"    
            }
            
        }
        stage("capture"){
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', followSymlinks: false
                jacoco()
                junit '**/target/surefire-reports/TEST*.xml'    
            }
        }
    }
    
    post {
        always {
            echo "URL de la construcción: ${env.BUILD_URL}"
            echo "Resultado actual: ${currentBuild.currentResult}"
            emailext body: "${env.BUILD_URL} \n ${currentBuild.absoluteUrl}", to: "soporte@jenkins.com", recipientProviders: [previous()],subject: "${currentBuild.currentResult}: Job:${env.JOB_NAME}"
        }
    }
}