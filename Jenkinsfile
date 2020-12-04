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
