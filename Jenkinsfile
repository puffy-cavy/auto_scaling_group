def STACK_NAME
def FULL_STACK_NAME
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
					FULL_STACK_NAME = 'aws cloudformation describe-stacks --query \'Stacks[*].[StackName]\' --output text | grep -m 1 $stackName'
					sh "aws cloudformation list-stack-resources --stack-name $fullStackName --query 'StackResourceSummaries[*].{ResourceType: ResourceType,PhysicalId: PhysicalResourceId, Status: ResourceStatus, LastUpdated: LastUpdatedTimestamp}'"

					}
				}
			}


		stage('QA'){
			steps{
				sh "echo [QA STAGE]"
			}
		}
	}
}
