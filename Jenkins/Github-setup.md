Pushing the code using the access token on the github would be something like this

```
git remote set-url origin https://<repo-name>:<MYTOKEN>@github.com/scuzzlebuzzle/ol3-1.git
```

providing the correct gitpath
This needs to be setted up as we 


And for installing git we generally do the `yum install git -y` as this is redhat

And then go to the JEnkins dashbaord --> Manage plugins --> available --> github
and add it and perform install without restart 

And then we need to add our github repo url in the job that we build after the maven setup is done .

We just head to the new_items in the job and then select a maven project give the build name as 'My First Maven Build' and then 
a. set SCM as git
b. set the repo to the Java Remote repository that has got pom.xml in it .
c. add the instructions in goals as `clean package install`
d. the in the build give pom.xml 

That's it the set up is done. For now i'm referring the repo url to be 
`https://github.com/prathap442/hello-world`
