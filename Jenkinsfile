pipeline 
{
    agent any

    stages 
    {
        stage('Sensitive Information') 
        {
            steps 
            {
                sh 'ls'
            }
        }
        stage('SCA') 
        {
            steps 
            {
                sh 'cd ..'
            }
        }
        stage('Code Review') 
        {
            steps 
            {
                sh 'ifconfig'
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
