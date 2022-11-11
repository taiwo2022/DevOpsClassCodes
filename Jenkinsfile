pipeline{
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
	agent none
      stages{
           stage('Checkout'){
              agent any
              steps{
		 echo 'cloning..'
                 git 'https://github.com/theitern/DevOpsClassCodes.git'
              }
          }
          stage('Compile'){
              agent any
              steps{
                  echo 'compiling..'
                  sh 'mvn compile'
	      }
          }
          stage('CodeReview'){
              agent {label 'slave1'}
              steps{
		    
		  echo 'codeReview'
                  sh 'mvn pmd:pmd'
              }
          }
           stage('UnitTest'){
              agent {label 'slave2'}
              steps{
	         echo 'Testing'
                  sh 'mvn test'
              }
               post {
               success {
                   junit 'target/surefire-reports/*.xml'
               }
           }	
          }
          stage('Package'){
              agent {label 'slave1'}
              steps{
                  sh 'mvn package'
              }
          }
      }
}
