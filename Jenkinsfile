pipeline{
	agent any
	stages{
		stage("Build"){
			steps{
				sh 'mkdir -p build'
				dir('build'){
					sh 'cmake3 ..'
					sh 'make'
					script{
						if(env.BRANCH_NAME == 'master'){
							sh 'make publish'
						}
					}
				}
			}
		}
	}
}
