pipeline {
		agent any
			stages {   

					stage ( 'Clone sources From GitHub' ) {								
							steps {
										git credentialsId: '0718e330-6d54-4bde-ae21-0402451752d3', url: 'https://github.com/venkeystore/Maven_Project.git'
									}	
						}		

	 //	stage ( 'static code analysis is performed in the Stage ' ) {								
	 //						steps {
	 //								withMaven (maven : 'M2_HOME_3.5' ) {
	 //									sh 'mvn sonar:sonar'
	 //										}
	 //							}	
	 //					}						

			stage ( 'Build Phase' ) {								
								steps {
										withMaven (maven : 'M2_HOME_3.5' ) {
											sh 'mvn clean pacakge'
												}
									}	
							}

			stage ( 'Code Coverage' ) {
								steps {
										jacoco()
									}		
								}
			stage ( 'Deployment Phase' ) {
								steps {
									sh ' sudo sshpass -p "$PASSWD" scp /home/ec2-user/epel-release-latest-7.noarch.rpm ec2-user@18.224.2.180:/home/ec2-user'
									}

								  }


								  
						}       // Stages End tag			
			}                 // Pipeline main tag
	