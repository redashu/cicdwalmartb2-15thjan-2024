# cicdwalmartb2-15thjan-2024

### job1 jenkins build step 

```
whoami
pwd
echo "this job will be fetching all the source code"
ls 
### testing apache maven version 
source ~/.bashrc 
mvn --version 
# build project
mvn install 
sleep 2
# check war file
ls target

### checking branch
mkdir  -p /tmp/ashunew/
cp -rf target/*.war /tmp/ashunew/
# cleaning build 
mvn clean 


```

### job 2 jenkins build steps 

```
ls -a
git branch -a

git checkout release
cp -rf /tmp/ashunew/*.war   .

git add .
git commit -m "updating war file"
git push https://redashu:password@github.com/redashu/ashu-walm-releaseb2.git

```

### starting with scripting of pipelines using jenkins 

<img src="jfile.png">


### sample jenkinsfile demo 1 

```
pipeline {
    agent any

    stages {
        stage('taking source code from git') {
            steps {
                echo 'pull code from github'
            }
        }
        // build stage
        stage('we are going to build code') {
            steps {
                echo 'yes we are now building'
            }
        }
        // pushing stage 
        stage('pushing build release') {
            steps {
                echo 'we are now pushing articarts to github'
            }
        }
    }
}

```

### sample file 2

```
pipeline {
    agent any

    stages {
        stage('taking source code from git') {
            steps {
                echo 'pull code from github'
                git branch: 'main', url: 'https://github.com/sivaa4232/mywebapp.git'
                sh 'ls -ltr' 
            }
        }
        // build stage
        stage('we are going to build code') {
            steps {
                echo 'yes we are now building'
            }
        }
        // pushing stage 
        stage('pushing build release') {
            steps {
                echo 'we are now pushing articarts to github'
            }
        }
    }
}

```
### adding stage build in jenkinsfile 

```
pipeline {
    agent any

    stages {
        stage('taking source code from git') {
            steps {
                echo 'pull code from github'
                git 'https://github.com/redashu/ashu-walm-mvnweb.git'
                sh 'ls -a'
                
            }
        }
        // build stage
        stage('we are going to build code') {
            steps {
                echo 'yes we are now building'
                sh '''
                    source ~/.bashrc 
                    mvn install 
                    ls target 
                    mkdir -p /tmp/newashudata/
                    cp -rf target/*.war  /tmp/newashudata/
                    mvn clean 
                '''
                
            }
        }
        // pushing stage 
        stage('pushing build release') {
            steps {
                echo 'we are now pushing articarts to github'
            }
        }
    }
}

```



