pipeline {

   // agent any
   		agent {
			label {
				label "master"
				customWorkspace "C:\\Program Files (x86)\\Jenkins\\workspace\\Test"
			}
		}
	
   parameters {  
       string(name: 'tomcat_dev', defaultValue: '18.191.184.219', description: 'Staging Server')

	   string(name: '*', defaultValue: '*', description: '*')
    }	

// triggers {
   //      pollSCM('* * * * *')
   //  }
              

			  
     tools {
        maven 'APACHE_MAVEN_3.5.0'  
        jdk 'Java_JDK_1.8'         
                                
           }

                                
stages{

//________________________________________________________________________________________________________________________________________
   //     stage('Checkout SCM'){
  //         steps {
   //         git credentialsId: '2c4b4347-5a8a-42df-b073-3c0ae71efb27', url: 'https://github.com/venkeystore/Maven_Project.git' 
   //       }
  //          }
//________________________________________________________________________________________________________________________________________

   
                                              
                                                
        stage('Build Phase'){
            steps {
                bat 'mvn clean package'                                                                                             											
                }
				
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
		
		
		
        stage('Static Code analysis'){
            steps {
			   bat 'mvn sonar:sonar'                                                                                         											
            }
        }		
		



        stage ('Deployments'){
            parallel{
                stage ('Deploy to test'){
                    steps {
						sh "scp ${perams.src}/*.war user@host_name:${params.dest_staging}/webapps"
                    }
                }

                stage ("Deploy to Staging"){
                    steps {
                        sh "scp ${perams.src}/*.war user@host_name:${params.dest_prod}/webapps"
                    }
                }
            }
        }
		

        stage('EmailNotification Phase'){
            steps {
                                                
				emailext body: 'Let analys your console ', subject: 'BuildNotification', to: 'venkateswara.mukkamalla@ivlglobal.com, Swamy.Kothuru@ivlglobal.com'
            }

        }		


    }
}
