pipeline
{
    agent any
    stages
    {
        stage('ContinuosDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContinuosBuild')
        {
            steps
            {
                sh 'mvn package'
            }    
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'e7cf90ed-4a8d-4d41-9064-663d7b54e081', path: '', url: 'http://172.31.93.73:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        
        }
        stage('ContinuosTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclerativePipeline/testing.jar'
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                input message: 'Required approvals', submitter: 'pridhvi'
                deploy adapters: [tomcat9(credentialsId: 'e7cf90ed-4a8d-4d41-9064-663d7b54e081', path: '', url: 'http://172.31.85.173:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
