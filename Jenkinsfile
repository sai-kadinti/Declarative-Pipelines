pipeline
{
    agent 
    {
        label 'built-in'
    }
    stages
    {
        stage ('Continuous-Download')
        {
            steps
            {
                git 'https://github.com/sai-kadinti/intelliQ-MavenJava.git'
            }
        }
        stage ('Continuous-Build')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage ('Continuous-Deployment')
        {
            steps
            {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'd34255da-6028-4b32-93d3-a47cdefbea39', path: '', url: 'http://172.31.87.13:8080/')], contextPath: 'scm-qa1', war: '**/*.war'
            }
        }
        stage ('Continuous-Testing')
        {
            steps
            {
                git 'https://github.com/sai-kadinti/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativeSCM/testing.jar'
            }
        }
        stage ('Continuous-Delivery')
        {
            steps
            {
                input message: 'Please approve the deployment', submitter: 'Manager'
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'd34255da-6028-4b32-93d3-a47cdefbea39', path: '', url: 'http://172.31.92.132:8080/')], contextPath: 'scm-prod1', war: '**/*.war'
            }
        }
        stage ('Post-Build')
        {
            steps
            {
                echo "Deployment succeeded access the link http://3.93.232.4:8080/scm/"
            }
        }
    }
}
