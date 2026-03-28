node 
{
    //   /var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven-3.9.6
   def mavenHome=tool name: "maven-3.9.14"
echo "git branch Name: ${env.BRANCH_NAME}"
echo "build number: ${env.BUILD_NUMBER}"

   try
   {  

     stage('Checkout Code') {
            git branch: 'dev', url: 'https://github.com/spandana-11/maven-webapplication-project-kkfunda.git'
        }

        stage('Maven Build') {
            sh "${mavenHome}/bin/mvn clean package"
        }

        stage('Sonar Report') {
            sh "${mavenHome}/bin/mvn sonar:sonar"
        }


   }  //try block end
   catch (e) {
   
       currentBuild.result = "FAILED"

  } finally {
    // Success or failure, always send notifications
    notifyBuild(currentBuild.result)       //function calling
  }

  
}  //node ending


def notifyBuild(String buildStatus = 'STARTED') {
  // build status of null means successful
  buildStatus =  buildStatus ?: 'SUCCESS'

  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    color = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESS') {
    color = 'GREEN'
    colorCode = '#278EF5'
  } else {
    color = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary, channel: '#practice-devops')
  
}
