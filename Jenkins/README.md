Connecting to the Aws EC2 using the pem file is simple

```
  chmod 400 <krishna>.pem
  ssh -i "~/Downloads/krishna.pem" ec2-user@<ec2-34.121.12121>
```

The above will make us connect to the ec2 once we are connected to the ec2 we do the following steps that are shown below .

First of all on taking amazon linuxec2 machine
- We need to install the java and find the home path environment for it and Jre folder which is the java run time environment .
- For installing java we do a 
```
  yum install java-1.8.*
```

- Once the java is installed by using the above command we need to set the java_home path but before that we need to find jvm and jdk path which would be installed in /usr/lib
```
 find /usr/lib/jvm/java-1.8.* | head -n 3
```

And the output of the above command would be 
```
  /usr/lib/jvm/java-1.8.0
  /usr/lib/jvm/java-1.8.0-openjdk
  /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.312.b07-1.amzn2.0.1.x86_64
```
We nee to set the java home path
```
$ export JAVA_HOME = /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.312.b07-1.amzn2.0.1.x86_64
```

Now instead of exporting we set the PATH variable in bash_profile by using 

```
  vi ~/.bash_profile
```

once the bash profile opens we need to modify as
```
    # .bash_profile

    # Get the aliases and functions
    if [ -f ~/.bashrc ]; then
        . ~/.bashrc
    fi

    # User specific environment and startup programs

    JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.312.b07-1.amzn2.0.1.x86_64
    PATH=$PATH:$HOME/bin:$JAVA_HOME

    export PATH
```

Now i need to install the jenkins so i have headed to download.jenkins.io
```
  yum install epel-release # repository that provides 'daemonize'
  yum install java-11-openjdk-devel
  yum install jenkins
```
have executed the above commands

To start the service of the jenkins we use
first check the status:
```
$ sudo service jenkins status
```
will give the output as inactive as we have not started yet the service
```
● jenkins.service - LSB: Jenkins Automation Server
   Loaded: loaded (/etc/rc.d/init.d/jenkins; bad; vendor preset: disabled)
   Active: inactive (dead)
     Docs: man:systemd-sysv-generator(8)
```

Now after  this we start using
```
 sudo service jenkins start
```

now if we check the status using `sudo service jenkins status` we will have something like this. 
```
● jenkins.service - LSB: Jenkins Automation Server
   Loaded: loaded (/etc/rc.d/init.d/jenkins; bad; vendor preset: disabled)
   Active: active (running) since Mon 2021-12-13 14:03:24 UTC; 3min 7s ago
     Docs: man:systemd-sysv-generator(8)
  Process: 4267 ExecStart=/etc/rc.d/init.d/jenkins start (code=exited, status=0/SUCCESS)
   CGroup: /system.slice/jenkins.service
           └─4271 /etc/alternatives/java -Djava.awt.headless=true -DJENKINS_HOME=/var/lib/jenkins -jar /usr/lib/jenkins/jenkins.war --logfile=/var/log/jenkins/jenkins.log --webroot=/var/cache/jenkins...

Dec 13 14:03:24 ip-thokkalo.ap-south-1.compute.internal systemd[1]: Starting LSB: Jenkins Automation Server...
Dec 13 14:03:24 ip-thokkalo.ap-south-1.compute.internal jenkins[4267]: Starting Jenkins [  OK  ]
Dec 13 14:03:24 ip-thokkalo.ap-south-1.compute.internal systemd[1]: Started LSB: Jenkins Automation Server.
```

Since jenkins runs on the port `8080`
And we have setted up the custom tcp rule of opening at 8080 we can basically access jenkins using public ip at that port.
```
  sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

So once we have the password we paste into the form for the access of the jenkins at port 8080
and click on submit 

and then we will click "X" as we don't need any suggested plugins or select plugins to install so we directly land at the jenkins dashboard .

Once we have landed at the jenkins dashboard we will click on the admin tab and change our password to 

```
 benkins
```
and since we are changing the intial Admin password so the username will be `admin`


======================================
We first add the JAVA_HOME path by going dashboard --> Manage Jenkins --> Global Tool Configuration and key value pairs as
```
  key: JAVA_HOME
  value: /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.312.b07-1.amzn2.0.1.x86_64
```

=======================================
Now once the jenkins installation and configuration of the JAVA_HOME path is done. Now we need to create the jobs we will create the first job using 

dashboard-->new items--> create an item --> Name: First_Job
Now we go to the build area ---> add Build Step--> in which we select `execute shell`
```
$ echo "Krishna says in geeta that human has his knowledge being covered by a smoke of fire name lust:):):)"
```
=========================================


Now once i had this job i had to run it manually that it the first mini job execution is done on the jenkins
