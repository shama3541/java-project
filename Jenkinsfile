pipeline {
   environment {
     git_url = "https://github.com/shama3541/java-project.git"
     git_branch = "master"
   }

  agent {label 'devslave1'}
 
  stages {
    stage('Pull Source') {
      steps {
        git credentialsId: '7019829d-4ca2-457c-b43a-1c740d3ca2b6', branch: "${git_branch}", url: "${git_url}"
       
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
                 withCredentials([usernamePassword(credentialsId: '20cb63c6-f1c0-484a-ab66-70b4d01d253b', passwordVariable: 'Password', usernameVariable: 'Username')]) {
                 sh "sudo docker login -u ${env.Username} -p ${env.Password}"
                 sh "sudo docker image tag myjava-image salilkul87/myjava-image:test"
                 sh "sudo docker image push salilkul87/myjava-image:test" 
               } 
             }  
          }
   //   stage('Deploy app') {
   //      steps {
    //        sh 'kubectl apply -f app-deploy.yaml'
    //     }
     // }
    }

//  post {
//    always {
//      deleteDir() /* cleanup the workspace */
//    }
//  }
  }
