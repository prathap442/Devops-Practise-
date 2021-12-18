So first of all since we have the jenkins being installed on a server and it is running their for tomcat server to run and have the war file deployed into it by jenkins once the build is done .


We first create the tomcat server using normal AWS way of creating amazon linux AMI and then what we do is first install the Apache tomcat version 8 on this particular server of tomcat .


For this we may need to add some commands

First ssh into the tomcat server using 
```
ssh -i "~/Downloads/prathap_jenkins_keypair.pem" ec2-user@xxxx2.amazonaws.com
```

Once we ssh then we download the tomcat from the apacher tomcat version 8. 
```
cd /opt
wget https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.73/bin/apache-tomcat-8.5.73.tar.gz
cd apache-tomcat-8.5.73

cd ..
mv apache-tomcat-8.5.73 tomcat #just for better naming convention the output of extracted tar file is just renamed to the tomcat
```


As we need to run tomcat which is a java based application we need to install java on our system .

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
$ export JAVA_HOME = /usr/lib/jvm/java-1.8.0-openjdk
```

Now instead of exporting we set the PATH variable in bash_profile by using 

```
  vi ~/.bash_profile
```


Now go to the Ipv4 public address and open the port 8080 like
```
http://<ipv4-address>:8080/
```
Now once we are able to access the application successfully see the cat icon of the Tomcat then click on the Managerapp it gives 403 Access Denied .



So now we get into the tomcat server and then
```
cd /opt/apache-tomcat-8.5.73
find / -name context
```
the output for the above find command would be 

```
/opt/apache-tomcat-8.5.73/conf/context.xml
/opt/apache-tomcat-8.5.73/webapps/examples/META-INF/context.xml
/opt/apache-tomcat-8.5.73/webapps/host-manager/META-INF/context.xml
/opt/apache-tomcat-8.5.73/webapps/manager/META-INF/context.xml
```

out of these files we modify the 
```
/opt/apache-tomcat-8.5.73/webapps/host-manager/META-INF/context.xml
/opt/apache-tomcat-8.5.73/webapps/manager/META-INF/context.xml
```
comment out the areas of the restriction of the Ip address

and then add the following users in the /opt/tomcat_folder/conf/tomcat-users.xml
```
 <role rolename="manager-gui"/>
 <role rolename="manager-script"/>
 <role rolename="manager-jmx"/>
 <role rolename="manager-status"/>
 <user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
 <user username="deployer" password="deployer" roles="manager-script"/>
 <user username="tomcat" password="s3cret" roles="manager-gui"/>
```


After the configuration changes are made we need to restart tomcat services. 
But this time it asks when accesse from the frontend 

