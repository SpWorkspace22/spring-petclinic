echo "Hello World"


node {
  
  stage("checkour"){
        sh "ls"
        git branch:"main", url: "https://github.com/SpWorkspace22/spring-petclinic.git"
        sh "ls" 
  }
  stage("build"){
        sh "./mvnw package"
  }
  stage("capture"){
        // **/target/*.jar
        archiveArtifacts artifacts: '**/target/*.jar'
        junit stdioRetention: '', testResults: '**/target/surefire-reports/TEST*.xml'
        jacoco()
  }
  stage("notification"){
        emailext subject: "${env.JOB_NAME}-${currentBuild.currentResult}",
        to: "sonuprasad@foo.com",
        recipientProviders: [previous()], 
        body: "The Build ${currentBuild.displayName} is ${currentBuild.currentResult} \n url : ${currentBuild.absoluteUrl}"
  }
}
