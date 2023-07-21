pipeline {
   environment {
     git_url = "https://github.com/salilkul/java-project.git"
     git_branch = "master"
   }

  agent any
 
  stages {
    stage('Pull Source') {
      steps {
        git credentialsId: '4e568653-41a2-4131-b9c0-2e512b61445a', branch: "${git_branch}", url: "${git_url}"
       
      }
     }
    
    stage('Maven Build') {
     steps { 
          sh "mvn clean package && cp target/*.jar . "
     }
    }
     
     stage('Docker Image Build') {     
        steps {
              sh 'sudo docker build -t myjava-image . '
               }
             }
        stage('Docker image push') {
           steps {
                 withCredentials([usernamePassword(credentialsId: 'b2674f2b-668e-4af0-9b33-dc80948a6230', passwordVariable: 'Password', usernameVariable: 'Username')]) {
                 sh "sudo docker login -u ${env.Username} -p ${env.Password}"
                 sh "sudo docker image tag myjava-image salilkul87/myjava-image:test"
                 sh "sudo docker image push salilkul87/myjava-image:test" 
               } 
             }  
          }
      stage('Deploy app') {
         steps {
            sh 'kubectl apply -f app-deploy.yaml'
         }
      }
    }

  post {
    always {
      deleteDir() /* cleanup the workspace */
    }
  }
  }
