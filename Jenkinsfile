pipeline
{
    agent 
    {
        label 'built-in'
    }
    stages
    {
        stage ('Continuos-Download')
        {
            steps
            {
                git 'https://github.com/sai-kadinti/intelliQ-MavenJava.git'
            }
        }
        stage ('Continuos-Build')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage ('Continuos-Deployment')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'd34255da-6028-4b32-93d3-a47cdefbea39', path: '', url: 'http://172.31.87.13:8080/')], contextPath: 'scm-qa', war: '**/*.war'
            }
        }
        stage ('Continuos-Testing')
        {
            steps
            {
                git 'https://github.com/sai-kadinti/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativeSCM/testing.jar'
            }
        }
        stage ('Continuos-Delivery')
        {
            steps
            {
                input message: 'Please approve the deployent', submitter: 'Manager'
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'd34255da-6028-4b32-93d3-a47cdefbea39', path: '', url: 'http://172.31.92.132:8080/')], contextPath: 'scm', war: '**/*.war'
            }
        }
        stage ('Post-Build')
        {
            steps
            {
                echo "Deployment succeed access the link http://3.93.232.4:8080/scm/"
            }
        }
    }
}
