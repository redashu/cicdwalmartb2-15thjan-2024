### Using ssh either from windows powershell or using mac terminal -- NO VPN please 

```
 ssh  ashu@18.235.217.86
ashu@18.235.217.86's password: 
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

-bash: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory
[ashu@ci-sever ~]$ 
[ashu@ci-sever ~]$ 
[ashu@ci-sever ~]$ whoami
ashu

```

### RHEL linux 

```
[root@ci-sever ~]# yum   install  git  -y
Failed to set locale, defaulting to C
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
amzn2-core                                                                                                                            | 3.6 kB  00:00:00     
Resolving Dependencies
--> Running transaction check
---> Package git.x86_64 0:2.40.1-1.amzn2.0.1 will be installed
--> Processing Dependency: git-core = 2.40.1-1.amzn2.0.1 for package: git-2.40.1-1.amzn2.0.1.x86_64
--> Processing Dependency: git-core-doc = 2.40.1-1.amzn2.0.1 for package: git-2.40.1-1.amzn2.0.1.x86_64
--> Processing Dependency: perl-Git = 2.40.1-1.amzn2.0.1 for package: git-2.40.1-1.amzn2.0.1.x86_64
--> Processing Dependency: perl(Git) for package: git-2.40.1-1.amzn2.0.1.x86_64
--> Processing Dependency: perl(Term::ReadKey) for package: git-2.40.1-1.amzn2.0.1.x86_64
--> Running transaction check
---> Package git-core.x86_64 0:2.40.1-1.amzn2.0.1 will be installed
---> Package git-core-doc.noarch 0:2.40.1-1.amzn2.0.1 will be installed
---> Package perl-Git.noarch 0:2.40.1-1.amzn2.0.1 will be installed
--> Processing Dependency: perl(Error) for package: perl-Git-2.40.1-1.amzn2.0.1.noarch
---> Package perl-TermReadKey.x86_64 0:2.30-20.amzn2.0.2 will be installed
--> Running transaction check
---> Package perl-Error.noarch 1:0.17020-2.amzn2 will be installed
--> Finished Dependency Resolution

```

### checking git version 

```
git version 
git version 2.40.1
[ashu@ci-sever ~]$ 

```

### Creating directory structure for future use 

```
[ashu@ci-sever ~]$ whoami
ashu
[ashu@ci-sever ~]$ pwd
/home/ashu
[ashu@ci-sever ~]$ mkdir  ashu-pipelines
[ashu@ci-sever ~]$ ls
ashu-pipelines
[ashu@ci-sever ~]$ mkdir  ashu-pipelines/{webapp,scripts,java,python}
[ashu@ci-sever ~]$ ls
ashu-pipelines
[ashu@ci-sever ~]$ ls ashu-pipelines/
java  python  scripts  webapp
[ashu@ci-sever ~]$ 
```

### converting a normal directory into git repo 

<img src="git1.png">

### git init process

<img src="git2.png">

### doing git init

<img src="gitinit.png">

### add using git -- start tracking data

```
[ashu@ci-sever webapp]$ ls
ashu.html
[ashu@ci-sever webapp]$ git add ashu.html 
[ashu@ci-sever webapp]$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   ashu.html

```

### in new git version we need to specify some details 

```
[ashu@ci-sever webapp]$ git commit -m  "first working code in webapp"
Author identity unknown

*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got 'ashu@ci-sever.(none)')

====>>>

[ashu@ci-sever webapp]$ 
[ashu@ci-sever webapp]$ 
[ashu@ci-sever webapp]$  git config --global user.email ashutoshh@linux.com
[ashu@ci-sever webapp]$ git config --global user.name   redashu
[ashu@ci-sever webapp]$

```

### now we can commit 

```
git commit -m  "first working code in webapp"
[master (root-commit) e9c831d] first working code in webapp
 1 file changed, 12 insertions(+)
 create mode 100644 ashu.html
[ashu@ci-sever webapp]$ 
```

