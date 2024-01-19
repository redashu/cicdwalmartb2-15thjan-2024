# cicdwalmartb2-15thjan-2024

### Revision 

<img src="rev.png">

### a little discussion about docker and container for code 

<img src="docker.png">

### Installing docker in jenkins server

```
yum install docker -y
Failed to set locale, defaulting to C
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
amzn2-core                                                                                                                            | 3.6 kB  00:00:00     
Resolving Dependencies



===>>
usermod -aG docker  jenkins 
[root@jenkins-server ~]# systemctl enable --now docker 
Created symlink from /etc/systemd/system/multi-user.target.wants/docker.service to /usr/lib/systemd/system/docker.service.
[root@jenkins-server ~]# 


===>>
chmod  777 /var/run/docker.sock 
```


### jenkinsfile to build docker image

```
pipeline {
    agent any

    stages {
        stage('testing docker connect') {
            steps {
                echo 'Hello World'
                sh 'docker version'
            }
        }
        // fetching git code 
        stage('taking git code and building it using docker') {
            steps {
                echo 'taking code'
                git branch:'master',url:'https://github.com/redashu/html-sample-app.git'
                sh 'ls'
                /*
                sh 'docker build -t walmashu:version1 . '
                sh 'docker images '
                */
                // using jenkins pipeline method 
                script {
                    def imageName = "ashutoshhwalmart"
                    def imageTag = "version1"
                    docker.build(imageName + ":" + imageTag, "-f Dockerfile .")
                }
                // verify image
                sh 'docker images '
                
            }
        }
    }
}

```


