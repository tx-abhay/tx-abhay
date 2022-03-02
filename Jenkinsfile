pipeline 
{
    agent any

    stages 
    {
        stage('Code Review') 
        {
            steps 
            {
                sh 'devskim analyze .'
                sh 'devskim analyze . output.json -f json'
            }
        }
        stage('SCA') 
        {
            steps 
            {
                sh 'sudo dependency-check.sh --scan .'
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
        stage('Open VAS - Infra Scan') 
        {
            steps 
            {
                echo 'abhay'
            }
        }
    }
}
