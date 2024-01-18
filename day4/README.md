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

### jenkinsfile with all 3 stages

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
                sh 'mkdir -p /tmp/ashu-relase'
                // changing location to avoid git conflict
                dir('/tmp/ashu-relase') {
                    git branch:'master',url:'https://github.com/redashu/ashu-walm-releaseb2.git'
                    sh ''' 
                        ls -a 
                        git branch -a
                        git checkout release 
                        cp -rf  /tmp/newashudata/*.war  . 
                        git add .
                        git commit -m "updating war in release via jenkinsfile"
                        git push https://redashu:password@github.com/redashu/ashu-walm-releaseb2.git
                    '''
                }
                
            }
        }
    }
}

```

### Deploy application using jenkins in 3 cases 

<img src="deploy.png">

### setting up passwordless / keybased auth between jenkins and tomcat server

### login to jenkins server 

```
 
➜  ~ ssh jenkins@18.210.25.241 
jenkins@18.210.25.241's password: 
Last login: Thu Jan 18 16:31:51 2024 from ip70-178-200-69.ks.ks.cox.net
   ,     #_
   ~\_  ####_        Amazon Linux 2
  ~~  \_#####\
  ~~     \###|       AL2 End of Life is 2025-06-30.
  ~~       \#/ ___
   ~~       V~' '->
    ~~~         /    A newer version of Amazon Linux is available!
      ~~._.   _/
         _/ _/       Amazon Linux 2023, GA and supported until 2028-03-15.
       _/m/'           https://aws.amazon.com/linux/amazon-linux-2023/

3 package(s) needed for security, out of 3 available
Run "sudo yum update" to apply all updates.
-bash: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory
-bash-4.2$ 
-bash-4.2$ 
-bash-4.2$ 
-bash-4.2$ 
-bash-4.2$ ls -l .ssh/
total 12
-rw------- 1 jenkins jenkins 1675 Jan 17 19:11 id_rsa
-rw-r--r-- 1 jenkins jenkins  404 Jan 17 19:11 id_rsa.pub
-rw-r--r-- 1 jenkins jenkins 1055 Jan 17 19:25 known_hosts
-bash-4.2$ 
-bash-4.2$ 
-bash-4.2$ ssh-copy-id   root@54.209.69.199
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/var/lib/jenkins/.ssh/id_rsa.pub"
The authenticity of host '54.209.69.199 (54.209.69.199)' can't be established.
ECDSA key fingerprint is SHA256:h49rVBfkTrTLKsJUyxuQkGL35gocABakG/eblj9Y1k0.
ECDSA key fingerprint is MD5:33:05:b6:48:a6:96:b8:cf:56:47:56:44:c6:c0:23:91.
Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@54.209.69.199's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'root@54.209.69.199'"
and check to make sure that only the key(s) you wanted were added.

-bash-4.2$ 



```




