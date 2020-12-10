pipeline{
		agent any
		stages {
			stage("check out"){
				steps{
					   checkout([$class: 'GitSCM', branches: [[name: '']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: "${env.GIT_URL}"]]])
					   sh label: '', script: '''
             #!/usr/bin/env bash
             WORKSPACE=$WORKSPACE
					   BRANCH=$BRANCH_NAME
					   GIT_BRANCH=$GIT_BRANCH
					   JENKINS_HOME=$JENKINS_HOME
					   BUILD_NUMBER=$BUILD_NUMBER
					   BUILD_ID=$BUILD_ID
					   JOB_NAME=$JOB_NAME
					   JOB_BASE_NAME=$JOB_BASE_NAME
					   EXECUTOR_NUMBER=$EXECUTOR_NUMBER
					   BUILD_TAG=$BUILD_TAG
					   NODE_NAME=$NODE_NAME
					   JENKINS_URL=$JENKINS_URL
					   BUILD_URL=$BUILD_URL
					   JOB_URL=$JOB_URL
					   GIT_COMMIT=$GIT_COMMIT
					   GIT_URL=$GIT_URL
					   GITVERSION=$(git rev-parse --short HEAD)
             '''
					   script {
					   		if ( env.GIT_BRANCH == "origin/dev") {               	
                	sh "sed -i 's/<ecr>/dev-art/' $WORKSPACE/*.yaml"
                	sh "sed -i 's/<repository>/dev-rep/' $WORKSPACE/*.yaml"
                	sh "sed -i 's/<artifactId>/dev-art/' $WORKSPACE/*.yaml"
                	sh "sed -i 's/<gitverion>/dev-git/' $WORKSPACE/*.yaml	"
                	sh "sed -i 's/<version>/dev-ver/' $WORKSPACE/*.yaml"
                }
                else if ( env.GIT_BRANCH == "origin/release") {           			
                	sh "sed -i 's/<ecr>/release-art/' $WORKSPACE/*.yaml"
                	sh "sed -i 's/<repository>/release-rep/' $WORKSPACE/*.yaml"
                	sh "sed -i 's/<artifactId>/release-art/' $WORKSPACE/*.yaml"
                	sh "sed -i 's/<gitverion>/release-git/' $WORKSPACE/*.yaml	"
                	sh "sed -i 's/<version>/release-ver/' $WORKSPACE/*.yaml"
                }
                else {           			
                  sh "echo 'new Branch'"
                }
             }
				}
			}
	}
}
