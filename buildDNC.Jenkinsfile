def dockerImage;

node('DockerBI')
{
    stage('SCM')
    {
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/menaNosshy/JenkinsDocker.git']]]);
    }

    stage('Build')
    {
        dockerImage = docker.build('mnyaqoub/agent-dnc:v' + env.BUILD_NUMBER, './dotnetcore');
    }

    stage('Push')
    {
        docker.withRegistry('', 'dockerhubcreds')
        {
            dockerImage.push();
        }
    }
}
