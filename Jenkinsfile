String branchName = "testDM"
String gitCredentials = "gitId"
String repoUrl = "https://github.com/Lakkahutta/jmeter_training.git"

node(){
 
 stage('Clone') {
      echo 'Cloning files from (branch: "' + branchName + '" )'
      dir('build') {
          git branch: branchName, credentialsId: 	gitCredentials, url: repoUrl
      }     
  }
 
 stage("configure") {

        sh "mkdir $WORKSPACE/$BUILD_NUMBER/"

    }

 

 stage('run test'){

 sh "mkdir -p /tmp/reports"

 sh "cd $WORKSPACE/apache-jmeter-5.5/apache-jmeter-5.5/bin"

 sh "$WORKSPACE/apache-jmeter-5.5/apache-jmeter-5.5/bin/jmeter -n -t build/MAKE-Order-Test.jmx -l /tmp/reports/JMeter.jtl -e -o /tmp/reports/HtmlReport"

 }

 

 stage('publish results'){

 sh "mv /tmp/reports/* $WORKSPACE/$BUILD_NUMBER/"

 archiveArtifacts artifacts: '$WORKSPACE/$BUILD_NUMBER/JMeter.jtl, $WORKSPACE/$BUILD_NUMBER/HtmlReport/index.html'

    } 
}
