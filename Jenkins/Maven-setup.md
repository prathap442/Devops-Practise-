Maven is basically a build tool which requires the pom.xml file

so we first login as root user in aws
```
 cd /opt
```

and then under opt we need to do `wget https://dlcdn.apache.org/maven/maven-3/3.8.4/binaries/apache-maven-3.8.4-bin.tar.gz` and then untar the tar file using

```
  tar -xzvf https://dlcdn.apache.org/maven/maven-3/3.8.4/binaries/apache-maven-3.8.4-bin.tar.gz
```

By doing the above command we will see that the folder is created `apache-maven-3.8.4`


Now that once the folder is setup we will change apache-maven-3.8.4 folder name to `maven`
for better naming convention

```
  $  mv apache-maven-3.8.4 maven
```

For the maven we need to setup 2 variables of Global 
```
  M2_HOME & M2
```

So same as the JAVA_HOME we do it here. open

```
  vi ~/.bash_profile
```

and we add the global variables of M2_HOME and M2

```
  M2_HOME=/opt/maven
  M2=/opt/maven/bin 
  PATH=$PATH:$HOME/bin:$JAVA_HOME:$M2_HOME:$M2
```


Now once this is added we logout and login back as root and check with the echo command

```
  echo $M2_HOME
```

```
  echo $M2
```

and verify the variable values and after that we need to go to the jenkins dashboard 
and then manage plugins 

and "maven_invoker" and "maven_integration" plugins
and install without restart