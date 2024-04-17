pipeline {
	agent any
	stages {
		stage("Git Checkout"){
			steps{
			    git credentialsId: 'github', url: 'https://github.com/Vivich007/Web3.git'
			}
		}
		stage("Configure Web Servers"){
			steps{
			    echo "Configure Web Servers"
				ansiblePlaybook credentialsId: 'Ansible-Project', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'Web_Calc_Servers.ini', playbook: '02-JavaTomcat.yml'
				
			}
		}
		
		stage("Maven Build"){
			steps{
			    echo "Build Maven Project"
				ansiblePlaybook credentialsId: 'Ansible-Project', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'Web_Calc_Servers.ini', playbook: '03-Maven_Build.yml', vaultTmpPath: ''
				
			}
		}
		
		stage("Maven Test"){
			steps{
			    echo "Test Maven Project"
				ansiblePlaybook credentialsId: 'Ansible-Project', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'Web_Calc_Servers.ini', playbook: '04-Maven_Test.yml', vaultTmpPath: ''
				
			}
		}
		
		stage("Deploy"){
			steps{
			    echo "Deploy Web App"
				ansiblePlaybook credentialsId: 'Ansible-Project', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'Web_Calc_Servers.ini', playbook: '05-Deploy.yml', vaultTmpPath: ''
				
			}
		}
	}
}
