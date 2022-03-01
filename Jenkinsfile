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
                sh ''
            }
        }  
        stage('Arachni - DAST') 
        {
            steps 
            {
                sh 'pwd'
            }
        }  
        stage('ZAP - DAST') 
        {
            steps 
            {
                sh 'ls -la'
            }
        }
         stage('Nikto - DAST') 
        {
            steps 
            {
                sh 'ifconfig'
                
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
