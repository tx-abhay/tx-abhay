pipeline 
{
    agent any

    stages 
    {
        stage('SCA') 
        {
            steps 
            {
                sh 'sudo dependency-check.sh --scan . -f XML -o .'
                sh 'curl -X POST "http://192.168.6.208:8080/api/v2/import-scan/" -H  "accept: application/json" -H  "Authorization: Token 3d1fca9401ab1ba00e542d0b9289b8a06c355703" -H  "Content-Type: multipart/form-data" -H  "X-CSRFToken: O96ALLXyBYbIDTMGcX80XAMSKoa8DevtFE4Yr4KRHZ4VgtKs14a1Yt2HJ5in30HW" -F "scan_date=2022-03-03" -F "minimum_severity=Critical" -F "active=true" -F "verified=true" -F "scan_type=Dependency Check Scan" -F "file=@dependency-check-report.xml;type=text/xml" -F "product_name=TX-DevSecOps" -F "engagement_name=AdHoc Import - Wed, 02 Mar 2022 11:43:15" -F "close_old_findings=false" -F "push_to_jira=false"'
            }
        }
        stage('Code Review Using SonarQube') 
        {
            steps 
            {
                sh '/opt/sonar/bin/sonar-scanner -Dsonar.projectKey=Testing -Dsonar.sources=. -Dsonar.host.url=http://192.168.6.208:9000 -Dsonar.login=cecd6d7e767c764d7576029905a6e334f43232ee -X'
                sh 'curl -X POST "http://192.168.6.208:8080/api/v2/import-scan/" -H  "accept: application/json" -H  "Authorization: Token 3d1fca9401ab1ba00e542d0b9289b8a06c355703" -H  "Content-Type: multipart/form-data" -H  "X-CSRFToken: O96ALLXyBYbIDTMGcX80XAMSKoa8DevtFE4Yr4KRHZ4VgtKs14a1Yt2HJ5in30HW" -F "scan_date=2022-03-03" -F "minimum_severity=Critical" -F "active=true" -F "verified=true" -F "scan_type=Dependency Check Scan" -F "file=@dependency-check-report.xml;type=text/xml" -F "product_name=TX-DevSecOps" -F "engagement_name=AdHoc Import - Wed, 02 Mar 2022 11:43:15" -F "close_old_findings=false" -F "push_to_jira=false"'
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
                sh 'sudo /root/devsecops/arachni/bin/arachni http://192.168.6.190/Vulnerable-Web-Application/homepage.html'
            }
        }  
        stage('ZAP - DAST') 
        {
            steps 
            {
                sh 'sudo docker run -t owasp/zap2docker-stable zap-baseline.py -t http://192.168.6.190/Vulnerable-Web-Application/homepage.html || true'
            }
        }
        stage('BURP - DAST') 
        {
            steps 
            {
                sh 'curl -vgw "\n" -X POST 'http://192.168.8.148:1337/v0.1/scan' -d '{"urls":["http://192.168.6.190/Vulnerable-Web-Application/homepage.html"]}''
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
