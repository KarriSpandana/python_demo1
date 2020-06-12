pipeline{
agent any
stages{
stage('SCM')
{
steps{
git 'https://github.com/devopstraining1990/python_demo1.git'
}
}
stage('Build')
{
steps{
sh 'python3 --version'
sh 'pip3 install --user -r requirements.txt'
}
}
stage('Install')
{
steps{
sh 'python3 --version'
sh 'pip3 install --user nose coverage nosexcover pylint'
//sh 'nose -sv --with-xunit-file=nosetests.xml --with-xcoverage-file=coverage.xml'
}
}

stage('Analysis')
{
steps{
withSonarQubeEnv('sonar') 
{
sh '/opt/sonar-scanner-3.3.0.1492-linux/bin/sonar-scanner -Dsonar.projectName=abc1 -Dsonar.projectVersion=2 -Dsonar.projectKey=abc1 -Dsonar.python.coverage.reportPath=coverage.xml -Dsonar.analysis.mode= -Dsonar.sources=.'
}
}
} 

stage('Test')
{
steps
{
   sh 'python3 test.py'
}
post
{
  always{
  junit 'test-reports/*.xml'
}
cleanup
{
   echo 'Clean up the workspace'
   deleteDir()/*clean up our workspace*/
}
}
}
}
}
