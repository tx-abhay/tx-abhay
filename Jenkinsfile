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

                sh 'curl -X POST "http://192.168.6.208:8080/api/v2/import-scan/" -H  "accept: application/json" -H  "Authorization: Token 3d1fca9401ab1ba00e542d0b9289b8a06c355703" -H  "Content-Type: multipart/form-data" -H  "X-CSRFToken: fbnssyFHyltk8UQHGje6fos8XAvdhqz56GlQ8Rs0EmmxLuOtvqg7ghIXWhDsHcLy" -F "minimum_severity=Info" -F "active=true" -F "verified=true" -F "scan_type=Dependency Check Scan" -F "file=@dependency-check-report_v5.2.0_webgoat8.xml;type=text/xml" -F "product_name=TX-DevSecOps" -F "engagement_name=DevSecOps-TX" -F "close_old_findings=false" -F "push_to_jira=false"'
            }
        }
        stage('Code Review Using SonarQube') 
        {
            steps 
            {
                sh '/home/testing/devsecops-tools/sonar/bin/sonar-scanner -Dsonar.projectKey=TX-DevSecOps -Dsonar.sources=. -Dsonar.host.url=http://192.168.6.208:9000 -Dsonar.login=973b03079dcffe8cda74174488d1d4e5146a8f65 -X'

                sh 'curl -X POST "http://192.168.6.208:8080/api/v2/import-scan/" -H  "accept: application/json" -H  "Authorization: Token 3d1fca9401ab1ba00e542d0b9289b8a06c355703" -H  "Content-Type: multipart/form-data" -H  "X-CSRFToken: fbnssyFHyltk8UQHGje6fos8XAvdhqz56GlQ8Rs0EmmxLuOtvqg7ghIXWhDsHcLy" -F "minimum_severity=Info" -F "active=true" -F "verified=true" -F "scan_type=SonarQube Scan" -F "file=@sonar-report-v1.1.0_java-tomcat_Sonarcloud-v8.0.0.485.html;type=text/html" -F "product_name=TX-DevSecOps" -F "engagement_name=DevSecOps-TX" -F "close_old_findings=false" -F "push_to_jira=false"'

            }
        }
        stage('Build') 
        {
            steps 
            {
                echo 'Application hosted on Local Server'
            }
        }  
        stage('ZAP - DAST') 
        {
            steps 
            {
                sh 'sudo docker run -t owasp/zap2docker-stable zap-baseline.py -t http://127.0.0.1:65412 || true'

                sh 'curl -X POST "http://192.168.6.208:8080/api/v2/import-scan/" -H  "accept: application/json" -H  "Authorization: Token 3d1fca9401ab1ba00e542d0b9289b8a06c355703" -H  "Content-Type: multipart/form-data" -H  "X-CSRFToken: fbnssyFHyltk8UQHGje6fos8XAvdhqz56GlQ8Rs0EmmxLuOtvqg7ghIXWhDsHcLy" -F "minimum_severity=Info" -F "active=true" -F "verified=true" -F "scan_type=ZAP Scan" -F "file=@zaproxy-wavsep_v1.4.0.1.xml;type=text/xml" -F "product_name=TX-DevSecOps" -F "engagement_name=DevSecOps-TX" -F "close_old_findings=false" -F "push_to_jira=false"'
            }
        }
    }
}
