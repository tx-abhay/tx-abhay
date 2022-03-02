pipeline 
{
    agent any

    stages 
    {
        stage('SCA') 
        {
            steps 
            {
                sh 'dependency-check.sh --scan .'
            }
        }
        stage('Code Review Using DevSkim') 
        {
            steps 
            {
                sh 'devskim analyze .'
                sh 'devskim analyze . output.json -f json'
            }
        }
        stage('Code Review Using SonarQube') 
        {
            steps 
            {
                sh '''
                sonar-scanner -Dsonar.projectKey=TX-DevSecOps -Dsonar.sources=. -Dsonar.host.url=http://192.168.6.208:9000 -Dsonar.login=cecd6d7e767c764d7576029905a6e334f43232ee
  				'''
            }
        }
        stage('Build') 
        {
            steps 
            {
                echo 'Application hosted on Local Server'
            }
        }  
        stage('Arachni - DAST') 
        {
            steps 
            {
                sh '/root/devsecops/arachni/bin/arachni http://192.168.6.190/Vulnerable-Web-Application/homepage.html'
            }
        }  
        stage('ZAP - DAST') 
        {
            steps 
            {
                sh 'sudo docker run -t owasp/zap2docker-stable zap-baseline.py -t http://192.168.6.190/Vulnerable-Web-Application/homepage.html || true'
            }
        }
         stage('Nikto - DAST') 
        {
            steps 
            {
                sh 'nikto -h http://192.168.6.190/Vulnerable-Web-Application/homepage.html'
                
            }
        }
    }
}
