def STACK_NAME
def DESIRED_CAPACITY
def MIN_SIZE
def MAX_SIZE

pipeline{
	agent any
	stages {
		stage('DEV'){
			steps{
				script{
					try{
						timeout(time: 5, unit: 'MINUTES'){
							STACK_NAME = input(id: 'stackName', message: 'Input stack name you want to query on', parameters: [[$class: 'TextParameterDefinition', defaultValue: '', description: '', name: '']])
							}
						}
					catch(e){
						echo('Skipping Updating Autoscaling group')
						throw e
						}
					try{
						timeout(time: 5, unit: 'MINUTES'){
							DESIRED_CAPACITY = input(id: 'desiredCapacity', message: 'Input desried capacity of the auto scaling group', parameters: [[$class: 'TextParameterDefinition', defaultValue: '', description: '', name: '']])
							}
						}
					catch(e){
						echo('Skipping Updating Autoscaling group')
						throw e
						}

					try{
						timeout(time: 5, unit: 'MINUTES'){
							MIN_SIZE = input(id: 'minSize', message: 'Input minimum size of the auto scaling group', parameters: [[$class: 'TextParameterDefinition', defaultValue: '', description: '', name: '']])
							}
						}
					catch(e){
						echo('Skipping Updating Autoscaling group')
						throw e
						}

					try{
						timeout(time: 5, unit: 'MINUTES'){
							MAX_SIZE = input(id: 'maxSize', message: 'Input maximum size of the auto scaling group', parameters: [[$class: 'TextParameterDefinition', defaultValue: '', description: '', name: '']])
							}
						}
					catch(e){
						echo('Skipping Updating Autoscaling group')
						throw e
						}

					}
					sh "export STACK_NAME"
					sh "export DESIRED_CAPACITY"
					sh "export MIN_SIZE"
					sh "export MAX_SIZE"
					sh """STACK_NAME=${STACK_NAME}"""
					sh """DESIRED_CAPACITY=${DESIRED_CAPACITY}"""
					sh """MIN_SIZE=${MIN_SIZE}"""
					sh """MAX_SIZE=${MAX_SIZE}"""
					sh "source jenkins_bash.sh" 
				}
			}


		stage('QA'){
			steps{
				sh "echo [QA STAGE]"
			}
		}
	}
}
