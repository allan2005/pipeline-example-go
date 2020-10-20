pipeline{
		agent any
		stages {
			stage('clone'){
				steps{
					git credentialsId: 'd546fc29-4399-40e5-95a5-aeaf5ec8cdbb', url: 'https://github.com/allan2005/jenkins-new-pub'
					script {
            build_tag = sh(returnStdout: true, script: 'git rev-parse --short HEAD').trim()
            repo_name = '699364278194.dkr.ecr.ap-southeast-1.amazonaws.com'
            app_name = 'jenkins-demo'
        	}
				}
			}
			stage('build'){
				steps{
					echo "2.Build Docker Image Stage"
					sh "docker build -t ${repo_name}/${app_name}:${build_tag} ."
				}
			}									
			stage('push'){
				steps{
					echo "3.Push Docker Image Stage"
					withDockerRegistry(credentialsId:'ecr:ap-southeast-1:0b248182-049b-4ff5-8a99-e29441e5ab23', url: 'https://699364278194.dkr.ecr.ap-southeast-1.amazonaws.com') {
						sh "docker push ${repo_name}/${app_name}:${build_tag}"
					}
				}
			}	
		}
}