pipeline {
    agent any
	
 environment{
        PATH = "/opt/apache-maven-3.9.9/bin:$PATH"
 }
	 
 stages {
      stage('checkout') {
           steps {
             
                git credentialsId: 'Password', url: 'https://github.com/Nagesh05021993/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn  clean package'             
          }
        }
        

        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t javatechie/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u javatechie -p ${dockerhubpwd}'

}
                   sh 'docker push javatechie/devops-integration'
                }
            }
        }
    }
}
