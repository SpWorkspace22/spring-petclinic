pipeline {
  agent any
  
  stages{
        // stage("checkout"){
        //     steps{
        //         sh "ls"
        //         git branch:"main", url: "https://github.com/SpWorkspace22/spring-petclinic.git"
        //         sh "ls"
        //     }
        // }
        stage("build"){
            steps{
                sh "./mvnw package"
            }
        }
        stage("capture"){
            steps{
                // **/target/*.jar
                archiveArtifacts artifacts: '**/target/*.jar'
                junit stdioRetention: '', testResults: '**/target/surefire-reports/TEST*.xml'
                jacoco()
            }
        }
    }
  
  post{
      always{
        emailext subject: "${env.JOB_NAME}-${currentBuild.currentResult}",
        to: "sonuprasad@foo.com",
        recipientProviders: [previous()], 
        body: "The Build ${currentBuild.displayName} is ${currentBuild.currentResult} \n url : ${currentBuild.absoluteUrl}"   
      }
    }
}
