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

