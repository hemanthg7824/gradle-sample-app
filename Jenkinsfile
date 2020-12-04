pipeline	{
	stages{
		stage('Build')	{
			steps {
			 script {
			  dir("test")
			  {
			  sh 'touch $WORKSPACE/Aritifact_$BUILD_NUMBER'
			  }
			  }
			 }
			}
			
		stage ('upload') {
			steps {
			 	rtupload (
				buildName: JOB_NAME,
				buildNumber:	BUILD_NMBER,
				serverId: SERVER_ID,
				spec: '''{
         			 "files": [
            			{
            			  "pattern": "/root/.jenkins/workspace/test02/*.war",
            			  "target": "Generic-demo-local/"
						  "recursive": "false"
            }
         ]
    }'''
	)
	}
	}
	  	stage('publish build info'
			steps {
			rtPublishBuildInfo (
				serverId: 'SERVER_ID,
		    	buildName: 'JOB_NAME',
    			buildNumber: 'BUILD_NUMBER'
			)
			}
			)
		stage ('Add interative promotion'){
		 steps {
		 	rtAddIneractivePromotion (
			serverId: SERVER_ID,
			targetRepo: 'Generic-demo-local/',
			displayName: 'Promote',
			buildName: 'JOB_NAME',
    		buildNumber: 'BUILD_NUMBER',
		    comment: 'test',
			sourceRepo: 'Generic-demo-local/',
			status: 'Released',
			inldeDependencies: true,
			failFast: true,
			copy: true
			)
			
			}
			}
			
			stage ('Removing files'){
			steps {
			 	sh 'rm -rf $WORKSPACE/*'
				}
				
			}
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
