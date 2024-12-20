# maven-nexus-sonarQube-demo
Integrating mvn with nexus and sonarQube


# Setup Prerequisite 

For this demo, create 3 ubuntu servers of size t3.medium,  with below specifications
- ensure instances are public 
- attach a keypair for ssh connections

a) Install Maven

    - tag instance : maven_demo

    NB: maven will run as background service so no ports on SG required
    
    Install JAVA (a prerequisite for Jenkins)

        sudo apt update && apt install openjdk-17-jre -y

    Verify Java Installation 
            java -version 

    Install Maven
        sudo apt install -y maven


b) Install Nexus
- tag instance: nexus

- use the install_nexus.sh script as userdata to install nexus

-  nexus is available on port default port 8081, open this port on SG attached to server

 - Access nexus on **http://`<server-pub-ip>`:`8081`** 

    
    ### configure nexus



c) Install SonarQube

- tag instance: sonarQube

- use the script sonarQube.sh to install sonarqube as userdata. 

- Sonarqube is avaiable on default port 9000. Allow this port on SG attaached to server.

- Access sonarqube on **http://`<server-pub-ip>`:`9000`** 


     ### configure nexus




# Demo

1) fork repo  https://github.com/mecbob/maven-nexus-sonarQube-demo/tree/main  and 

update the following detains in settings.xml and pom.xml files.  (use gitHub UI for the updates)
    - nexus credentials
    - IPs for the nexus and sonarServer

2) clone your repo on the maven server, where mvn can build the javabased project. 

4) Create a simple Java project using 

    mvn archetype:generate -DgroupId=com.example.demo -DartifactId=demoApp -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.5 -DinteractiveMode=false

3) cd into the Java project directory **demoApp** (folder with pom.xml and src directory)

4) build and push the maven artifact to nexus using the deploy [build lifecycle](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html) command.
    mvn clean deploy 



