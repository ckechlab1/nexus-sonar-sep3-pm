
pipeline {
    agent any

    // triggers {
    //     // Polls the SCM every minute using cron syntax:
    //     pollSCM('* * * * *') 
    // }
    
    tools {
        maven "M3"
    }

	environment {
		pom = readMavenPom(file: 'calculator/pom.xml')
		artifactId = pom.getArtifactId()
		version = pom.getVersion()
		name = pom.getName()
		groupId = pom.getGroupId()
	}

    stages {
        stage('Check Git pull') {
            steps {
                sh 'ls -l'
				sh 'rm -rf /root/.m2/repository/*'   
            }
        }

		stage('Build') {
		steps {
			dir('calculator') {
			sh 'cat src/main/java/com/echios/App.java '
			sh 'mvn clean install'
			}
		}
		}

		stage('Environment details') {
		steps {
			dir('calculator') {
			script {
				echo "Version: ${version}"
				echo "Group ID: ${groupId}"
				echo "Artifact ID: ${artifactId}"
			}
			}
		}
		}

        stage('SonarQube Analysis...') {
            steps {
                dir('calculator') {
                    script {
                        withSonarQubeEnv(credentialsId: 'sonar-scan') {
                        sh 'mvn clean package sonar:sonar -Dsonar.coverage.exclusions=**/*'
                        }
                    }
                }
            }
        }

        stage('Send to Nexus snapshot repo') {
            steps {
                dir('calculator') {
                echo 'Nexus upload'
                nexusArtifactUploader(
                    credentialsId: 'nexus-jenkins',
                    groupId: "${groupId}",
                    nexusUrl: 'YOUR_GITHUB_NEXUS_URL-8081.app.github.dev',
                    nexusVersion: 'nexus3',
                    protocol: 'https',
                    repository: 'echop',
                    version: "${version}",
                    artifacts: [
                        [
                            artifactId: "${artifactId}",
                            classifier: '',
                            file: "target/${artifactId}-${version}.jar",
                            type: 'jar'
                        ]
                    ]
                )
                }
            }
        }

// stages finish
    }
}
